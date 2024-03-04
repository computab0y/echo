# Admin Onboarding Guide

# Configuring a namespace / onboarding a new team

Each of the following steps must be done per namespace being created (must be repeated for child namespaces).

### Legend:

You will notice multiple commands with values encapsulated in <>, these are to be replaced with the values are required by your environment and needs. Please see the Legend below for an explaination of each of these. 

`<namespace>` = [namespace](https://www.vaultproject.io/docs/enterprise/namespaces) inside of vault to be created and managed.

`<k8-vault-namespace>` is the kubernetes namespace which vault is installed on. 

`<vault-name>` is the name of the helm name used during the installation of vault. It will bootstrap multiple environmental names (pods, SDN entries etc.)
## Namespace creation 

To create a namespace simply run the following command:

```bash
# Connect to the <vault-name>-0 pod on the <k8-vault-namespace> namespace
oc project <k8-vault-namespace>
oc rsh <vault-name>-0

# Namespace creation
vault namespace create <namespace>
```
## Kubernetes Authentication 

The following steps must be followed for our Kubernetes cluster to use our Vault Secrets

**NOTE: The following must be run inside of `<vault-name>-0`**

```bash
# Connect to the <vault-name>-0 pod on the <k8-vault-namespace> namespace
oc project <k8-vault-namespace>
oc rsh <vault-name>-0

# Enable Kubernetes Authentication on the required namespace
vault auth enable -namespace=<namespace> kubernetes

# Use the service account used by the Vault pod to authenticate against other request via Kubernetes 
vault write -namespace=<namespace> auth/kubernetes/config  token_reviewer_jwt="$(cat /var/run/secrets/kubernetes.io/serviceaccount/token)"  kubernetes_host="https://$KUBERNETES_PORT_443_TCP_ADDR:443" kubernetes_ca_cert=@/var/run/secrets/kubernetes.io/serviceaccount/ca.crt issuer=https://kubernetes.default.svc

```

## RH-SSO (OIDC)

### Configuring OIDC 

The following steps must be followed for this namespace to be accessable by team members via RedHat SSO (RH-SSO).

Additionally, you must be provisoned by the platform admin with a `CLIENT ID` and `CLIENT SECRET` along with the base path that RedHat SSO is accessible from. 

Groups mapping should only be done per namespace requiring it (i.e. team2 groups should be added to team2 namespace, but not to team1)

**NOTE: The following must be run inside of `<vault-name>-0`**
```bash

# Run the following inside of <vault-name>-0 (can be accessed via oc rsh <vault-name>-0 assuming you are on the correct namespace)

# 0. Enable the OIDC Authentication Method
vault auth enable -namespace=<namespace> oidc

# 1. Write a default policy for what a user without any groups should be able to see
# NOTE: You must not name this 'default' as that is a reserved name. Vault will not warn you if you do try to do so though.
# NOTE: This policy must remain empty to restrict default access to allow for no access.
vault policy write -namespace=<namespace> reader - << EOF

EOF

# 2. Configure OIDC Authentication with the RH-SSO OIDC Credentials
vault write -namespace=<namespace> auth/oidc/config \
         oidc_discovery_url="https://{RH-SSO_BASE_PATH}/auth/realms/sso" \
         oidc_client_id="{VAULT_CLIENT_ID}" \
         oidc_client_secret="{VAULT_CLIENT_SECRET}" \
         default_role="reader"

# 3. Bind a default role (reader)
# Note: mapping groups_claim="groups" means that we expect to see a "groups" object in the ID Token from RH-SSO. In the coming steps we use values from this and map their names against Vault Policies to restrict access.
vault write -namespace=<namespace> auth/oidc/role/reader \
      bound_audiences="{VAULT_CLIENT_ID}" \
      allowed_redirect_uris="https://{VAULT_BASE_PATH}/ui/vault/auth/oidc/oidc/callback" \
      user_claim="sub" \
      groups_claim="groups" \
      policies="reader"

```

### **Configuring a RH-SSO Group**

The following must be repeated for each 'group' created on RedHat SSO that is relavent to the current namespace
The following is for an example group 'engineering-admin' who has superuser privillages. Please replace 'engineering-admin' as required by your needs. 

Please additionally take a look at configuring [policies](https://www.hashicorp.com/resources/policies-vault) to configure access policies as required.  

```bash
# Creation of an engineering-admin policy with super user privillages 
# Note: The example policy below will allow an admin to self-govern their privillages.
vault policy write -namespace=<namespace> engineering-admin - << EOF

# Manage namespaces
path "sys/namespaces/*" {
   capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

path "sys/capabilities"
{
  capabilities = ["create", "update"]
}

path "sys/capabilities-self"
{
  capabilities = ["create", "update"]
}

# Manage policies
path "sys/policies/acl/*" {
   capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

path "sys/policies/acl" {
   capabilities = ["create", "read", "update", "delete", "list"]
}

path "sys/policies/rgp/*" {
   capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

path "sys/policies/egp" {
   capabilities = ["create", "read", "update", "delete", "list"]
}

path "sys/policies/egp/*" {
   capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

path "sys/policies/rgp" {
   capabilities = ["create", "read", "update", "delete", "list"]
}

# Enable and manage secrets engines
path "sys/mounts/*" {
   capabilities = ["create", "read", "update", "delete", "list"]
}

# List available secrets engines
path "sys/mounts" {
  capabilities = [ "create", "read", "list" ]
}

# Create and manage entities and groups
path "identity/*" {
   capabilities = ["create", "read", "update", "delete", "list"]
}

# List, create, update, and delete auth backends
path "sys/auth"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

path "auth/*" {
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

# Manage secrets at 'kv'
# NOTE: Replace/extend this with whatever secret engines are being used in this namespace. 
path "kv/*" {
   capabilities = ["create", "read", "update", "delete", "list"]
}
EOF

# The following must be run inside the leader pod. You can run `oc rsh <vault-name>-0` to access the pod
# mount_accessor and canonical_id are required to Bind the External Group to the OIDC Authentication Method

# 4.1 Get a list of the authentication methods for the required namespace 
vault auth list -namespace=<namespace> -format=json
```

*Example Output* 
```json
{
  "kubernetes/": {
    ...
  },
  "oidc/": {
    "uuid": "54b6aa1b-7722-1df1-1b95-348056842aeb",
    "type": "oidc",
    "description": "",
    "accessor": "auth_oidc_1ceb0731",
    "config": {
      ...
    },
    ...
  },
  "token/": {
    ...
  }
}
```

```bash
# 4.2 Get the unique ID for the OIDC authentication method
MOUNT_ACCESSOR=auth_oidc_1ceb0731 # Take the value of oidc.accessor from the output of previous command

# 4.3 Create an External Group in Vault that maps to the name of a group defined in RH-SSO
vault write -namespace=<namespace> -format=json identity/group name="engineering-admin" type="external" policies="engineering-admin"

```

*Example Output* 
```json
{
  "request_id": "14c4c47b-056c-d709-8224-01215d15f8d6",
  "lease_id": "",
  "lease_duration": 0,
  "renewable": false,
  "data": {
    "id": "b930bb7e-c7be-1928-5db9-162e6bf86ab6",
    "name": "test-1"
  },
  "warnings": null
}
```

```bash
# 4.4. Get the unique ID for the newly created External Group
CANONICAL_ID=b930bb7e-c7be-1928-5db9-162e6bf86ab6 # Take the value of data.id from the output of previous command


# 4.5. Bind the External Group to the OIDC Authentication Method
vault write -namespace=<namespace> -format=json identity/group-alias name="engineering-admin"  mount_accessor=$MOUNT_ACCESSOR canonical_id=$CANONICAL_ID
```

*Example Output* 
```json
{
  "request_id": "10cfb3ab-fc64-86e7-5c36-e7052972a9eb",
  "lease_id": "",
  "lease_duration": 0,
  "renewable": false,
  "data": {
    "canonical_id": "b930bb7e-c7be-1928-5db9-162e6bf86ab6",
    "id": "41f38be2-da17-cb13-8cc4-019cf9b626ef"
  },
  "warnings": null
}
```

```bash
# You should now be able to log in as a user with the 'engineering-admin' 
```
