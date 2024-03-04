                                                                  
## DevSecOps Best Practices (Draft) ##


## Contents

[1. Secure application development process](#secure-application-development-process)

[2. Use secrets management tool](#Use-secrets-management-tool)

[3. Container Image Build ](#Container-Image-Build)

[4. Choosing scanning tools ](#Choosing-scanning-tools)

[5. Resource requirement ](#Resource-requirement )

[6. Image Repository ](#Image-Repository )

[7. GitOps (Deployment) tool ](#GitOps-tool )

[8. Best Practises](#Best-practises )

##

### Secure application development process
The first step to securing your DevOps pipeline is to ensure that your application development process is secure. This means ensuring that only authorized developers have access to your code repositories and that all code changes are reviewed and approved by a qualified reviewer before being merged into the main branch. It also helps to have developers that you trust to do the job properly and to observe cybersecurity best practices throughout.

Project team branching strategy be in place to maintain the different code base as per environments, such that environment specific testing.

Example : System Integration (SIT) Test, Performance Test and User Acceptance (UAT) Test etc.

### Use secrets management tool
A secret is a piece of sensitive information that should be kept confidential, such as a personal access token (PAT). Secrets management is the process of securely storing and managing secrets in order access various DevOps tools.
The secrets management tool, such as Hashicorp’s Vault can help to manage secrets centrally and provides access control & auditing capabilities.
Access token are stored in structure way in vault for the pipeline to access the tools such as GIT, SonarQube and Quay.

### Container Image Build 
Various tools are available on the platform. Application team is required to choose the right tool, based application code. 

Example tools such as Buildah, can greatly increase the speed of builds and reduce the number of resources required to support a build farm.


### Choosing scanning tools.
Choosing the right tool as part of the pipeline to identify vulnerabilities early phase in project life cycle.

SonarSource for continuous inspection of code quality. SonarQube does static code (SAST) analysis, which provides a detailed report of bugs, code smells, vulnerabilities, code duplications. Project team required to define Quality gate as per project needs.
OWASP Zed Attack Proxy (ZAP) for Web Application Penetration Testing.
RHACS is the runtime container scanning tool on Redhat platform. Project team required to monitor for CVEs in the namespace and running container image / application.


### Resource requirement 
If the project team does not define resource requirement in order perform the task than Openshift Platfrom applies default resources for the tasks these may slow down builds or fail perform task if there is higher resource requirement.

Here is the Example spec to define resources as part of yaml file for the task.
 
    - name: sonar-scan
      resources:
        requests:
          memory: 1Gi
          cpu: 1
        limits:
          memory: 2Gi
          cpu: 2
### Image Repository  
Red Hat Quay container registry platform provides secure storage, distribution, and governance of containers and cloud-native artifacts on any infrastructure. It is setup to run on top of Red Hat OpenShift, Images which are stored on Quay get scanned by in built-tool called Clair nd report the CVE's.

### GitOps (Deployment) tool.
ArgoCD is preferred deployment tool on D2S platform and project team can configure such way that whenever there is change in image or when new version of image is created then ArgoCD automatically detect the updated metadata file start deployment.

### Best Practises

The D2S service and platform is optimised for developing modern, cloud native apps that align to MOD's future architecture vision. Whilst we frequently spotlight 12-factor style, progressive web apps are what we expect to be developed, we want to highlight the importance of zero trust principles on the D2S.Historically, MOD applications and services have trusted the network, assuming any service or user that can 'see' the service is a legitimate user. As you'll be aware, this is a hugely problematic and widely discredited approach; legacy apps written this way are a significant constraint on our efforts to improve user experience. New software, including that written using D2S is expected to follow Zero Trust principles, focusing on identity as its main security 'perimeter', in almost all cases requiring users to be authenticated and continuously validated. D2S, in line with this and the Cloud First policy and Foundry ways of working uses the Internet as its primary network.Consequently, application endpoints in both dev/test and production namespaces are available on the Internet by default. This follows the zero trust and openness principles. At the start of our private beta we have been limiting access to certain IP address whilst we developed improved security monitoring. IP limits have caused significant difficulties for some users and we are now in a position to disable this workaround. We will remove this filtering in the next business day.Shared responsibility model on application security:- DevOps teams are responsible for checking their applications/containers to make sure they're applying zero trust principles (i.e. that they're requiring authentication, unless they're specifically designed to put information/services into the public domain).

-  DevOps teams are responsible for reviewing the strength of controls for your applications, ensuring measures like multi-factor authentication are in place.

Best practise Reference doc:  https://www.ncsc.gov.uk/collection/zero-trust-architecture 
