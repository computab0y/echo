# Document Purpose #
Purpose of this document is to provide a new user, who is onboarding onto the Foundry OpenShift Platform (on MOD iACE), a sequence of steps to follow to access to the following applications:

•	OpenShift Console

•	Grafana

•	Kibana

•	Red Hat Advanced Cluster Security (RHACS)

Please note, this is not a guide on how to use the application. 
Please see the reference section of this document for more information on how to use the applications mentioned above. 

# Pre-Requirements #
•	User will have a Defence Digital Service (DDS) Google email account.

•	User has provided their static MOD machines IP Address to the Azure Administrator. This will be added to the WAF access list to allow access to the OpenShift console.

•	User has reviewed the User Guide available on GitHub:

    o	https://github.com/defencedigital/dso-scm

•	For creation and access to namespace/ project, the application team lead has logged onto the OpenShift console and created the said namespace/ project. See team lead steps described in this document.

# References #
•	OpenShift Console: https://access.redhat.com/documentation/en-us/openshift_container_platform/4.9/html/web_console/index

•	RHACS: https://docs.openshift.com/acs/3.67/welcome/index.html

•	Grafana: https://grafana.com

•	Kibana: https://www.elastic.co/kibana/

# Application Team User Onboarding Steps #
•	The user has logged in to their Google DDS account.

•	The user opens the OpenShift Console and logs in using their Google DDS account to provide authentication:

    o	Logon to the OpenShift Console using this link: https://console-openshift-console.apps.ocp1.azure.dso.digital.mod.uk

    o	Click on the ‘rh-sso’ option:

![](./images/OCP1.PNG)

On a second screen, the user will be promoted to choose logon method. Choose the 'Google' option.

![](./images/OCP2.PNG)

If not already logged into user’s DDS Google account, enter DDS account credentials:

![](./images/OCP3.PNG)

•	Once logged in, the user will see the OpenShift console landing page. Access to create and view namespaces/ projects will be limited until the application team lead has created namespaces/ projects and allowed access to the rest of the team (see instructions below).

•	Email dso.support@digital.mod.uk to confirm user has logged in for the first time and request the Platform administrator to setup profile and add to the team’s user group. In the email, describe this is your first time login and describe the name of the team the user belongs to.

•	On confirmation from the Platform administrator, that user profile has been setup, login to the OpenShift console. The user may or may not have additional permissions to access to access OpenShift functionalities, dependant on the users team and role/ responsibilities.

•	A view of the OpenShift console is illustrated below.

![](./images/OCP4.PNG)

•	Click on any project that has been created and the console will show an overview of the project’s status in the console:

![](./images/OCP5.PNG)


# Monitoring #

•	The OpenShift platform provides monitoring capabilities from within the OpenShift console. Where a namespace and an application pod has been created, the user can access monitoring of the pod, see illustration below.

![](./images/OCP6.PNG)

•	Where Grafana has been setup for the project, open the URL of the Grafana dashboard.

Note, Grafana capability needs to be requested per project. The request can be made from the platform administrator by emailing the support team at dso.support@digital.mod.uk

![](./images/OCP7.PNG)


# Kibana #

•	To access Kibana, open the following URL (while logged into the OpenShift console and within the same browser instance):

    o	https://kibana-openshift-logging.apps.ocp1.azure.dso.digital.mod.uk/

![](./images/OCP8.PNG)

•	Kibana will pull metrics for the project created in OpenShift. 
•	The menu in the left pane will allow navigation through the application options and allow user to capture metrics captured from application containers.

![](./images/OCP9.PNG)


# RHACS #

•	Red Hat Advanced Cluster Security (RHACS) can be access from the following URL (while logged into the OpenShift console and within the same browser instance):

    o	https://central-stackrox.apps.ocp1.azure.dso.digital.mod.uk

![](./images/OCP10.PNG)

•	Access to RHACS should be requested from the platform administrator by emailing the support team at dso.support@digital.mod.uk.


# Application Lead User Guide #

•	The application lead will be given privileges to create namespaces/ projects on the OpenShift platform. They can create projects and allow other members of their team access to those projects.

•	An application lead must identify themselves to the platform administrator, who will elevate the application leads user profile with the enhanced privileges. They can make a request by emailing the support team here: dso.support@digital.mod.uk

•	Once the application lead has be granted the enhanced privileges, they can create a project within the OpenShift console:

![](./images/OCP11.PNG)


•	To allow access to this project to other members of the team, navigate to User Management -> Rolebindings

![](./images/OCP12.PNG)

•	Click on Create binding and fill out the details on the form as illustrated with the example below.

![](./images/OCP13.PNG)

•	Name: chose a unique name for the role-binding

•	Namespace: the drop down will display only those namespace/ project created or available to application lead. Choose the one that is needed for providing access to the team.

•	Role: Choose a role to assign.

    o	This can be ‘admin’ for highest level of privileges or a role with less privileges.

•	Subject Name: Choose ‘Group’ as the subject and list the name of the group.

    o	The name of the application teams group will be confirmed by the platform administrator at time of request to be made the application teams group lead.

    o	If this is unknow, please contact support team by emailing dso.support@digital.mod.uk

•	Click on Create to confirm the transaction.

•	The entire team will now have access to the project.

•	If access is to be granted to a particular team member, chose ‘User’ as the Subject Name from the Create Rolebinding page and add the username of the team member.







