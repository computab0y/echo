Red Hat Quay container registry platform provides secure storage, distribution, and governance of containers and cloud-native artifacts on any infrastructure. It is setup to run on top of Red Hat OpenShift.

Follow the below steps as a Team Lead or a Developer to get started with managing and using Quay.

# Quay Onboarding – Team Lead

**1. Log in to Quay (through RH-SSO)**. OpenShift Quay can be accessed [here](https://dso-quay-registry-quay-quay-enterprise.apps.ocp1.azure.dso.digital.mod.uk/organizations/new/).

Click on the above link (highlighted) to connect using your RH SSO credentials.

![](./images/RackMultipart20220113-4-61adqd_html_44a25a6bff5df3c3.png)

Add username and password provided to you by the platform admin on the screen below. You will be required to change your password if logging in for the first time.

![](./images/RackMultipart20220113-4-61adqd_html_bbf9b0f5bb93e3a0.png)

**2. Create Quay Organisation** by opening below [page](https://dso-quay-registry-quay-quay-enterprise.apps.ocp1.azure.dso.digital.mod.uk/organizations/new/). Add appropriate organisation name following naming convention relevant to your team. E.g mod-dev-team-a

![](./images/RackMultipart20220113-4-61adqd_html_aa3504b45b005402.png)

**3. Create Teams(groups)** for Team Leads and developers.

Once Organisation is created, click on the organisation from the home page

![](./images/RackMultipart20220113-4-61adqd_html_c560e4b2c15cf213.png)

Click on the teams and membership tab and click on &quot;Create New Team&quot;

![](./images/RackMultipart20220113-4-61adqd_html_3b681998d9a70ea9.png)

As shown above (1) an Admin Group with admin role is created. (2) a developer team with member role is created. (use appropriate naming convention for the group of your team)

**4. Create Robot Account** to be used by pipeline

Click on the robot accounts tab and click on the &quot;Create Robot account&quot;

![](./images/RackMultipart20220113-4-61adqd_html_b37dc8ccd8e55054.png)

As can be seen above a robot\_team\_a account is created. (Use account name relevant to your project)

Clicking on the account name displays the credentials for the robot account to configure a secret to be used on the pipelines. There is also option to regenerate new token for the robot account.

![](./images/RackMultipart20220113-4-61adqd_html_efffbab995d46869.png)

## Pull secret:

Create Kubernatives pull secret with secret .dockerconfigjson
![](./images/kube-pull-secret.png)

Create secret on ocp and add it to the pipleline and default service accounts.


Example screenshot
![](./images/pull-secret.png)

## Add Pull secret to Service account

Add secret to pipleline and default accounts under ImagePullSecret

Example screenshot
![](./images/add-pull-secret-service-account.png)


**5. Create Repository** to be used by application

NOTE: the repository name needs to be the same as the application name.

Click on the &quot;Create New Repository&quot; button on the home page as highlighted below

![](./images/RackMultipart20220113-4-61adqd_html_34a206136a1ca9a9.png)

Below screen shows the details required on creating new repository. (1) ensure you select the correct organisation from the drop down. (2) Add a repository name. (3) Add repo description if required (4) select on repository visibility Public/Private

![](./images/RackMultipart20220113-4-61adqd_html_71199fa3313d6e05.png)

**6. Assign Developer Team(group)** (Read-Only) permission to repos. Assign robot account permission (Write) to repos

Once Repository is created, from Quay home page, click on the repository name to setup permission as shown below

![](./images/RackMultipart20220113-4-61adqd_html_84bb938622cd9007.png)

Go to the repository settings tab to add teams, update permissions.

![](./images/RackMultipart20220113-4-61adqd_html_36f13c530d838b98.png)

To add Teams, you can use the field below. The pre-created Teams (admin, developer) are listed here for ease of selection.

![](./images/RackMultipart20220113-4-61adqd_html_47ce70d68d4949e2.png)

**7. Add or remove Team members** to the group

Go to the organisation home page by clicking the list from Quay home page as shown below.

![](./images/RackMultipart20220113-4-61adqd_html_ef8febfa0e659e41.png)

Go to the &quot;Teams and membership&quot; tab and select the appropriate team name as shown below.

![](./images/RackMultipart20220113-4-61adqd_html_d8d0321ccabc6e0e.png)

The below screen shows the Team settings to add users, robot account or remove as required. To add users use the Team member search field.

![](./images/RackMultipart20220113-4-61adqd_html_465869d033e1a9e9.png)

# Quay Onboarding – Developer

**1. Log in to Quay (through RH-SSO)** . OpenShift Quay can be accessed [here](https://dso-quay-registry-quay-quay-enterprise.apps.ocp1.azure.dso.digital.mod.uk/organizations/new/).

Click on the link below (highlighted) to connect using your RH SSO credentials.

![](./images/RackMultipart20220113-4-61adqd_html_44a25a6bff5df3c3.png)

Add username and password provided to you by the platform admin on the screen below. You will be required to change your password if logging in for the first time.

![](./images/RackMultipart20220113-4-61adqd_html_bbf9b0f5bb93e3a0.png)

Once connected your organisation is visible as shown below:

![](./images/RackMultipart20220113-4-61adqd_html_c860deb4a948627.png)

Repository is listed below:

![](./images/RackMultipart20220113-4-61adqd_html_d81891920e860dc5.png)

Clicking on the repository name, its possible to view repository activity, Application Tags (versions) that&#39;s are pushed to this repository and tag history.

![](./images/RackMultipart20220113-4-61adqd_html_2648b1e78c82800b.png)
