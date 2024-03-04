# Personal Access Token's (PATs) #


Personal access tokens (PATs) are an alternative to using passwords for authentication to GitHub when using the GitHub API or the command line.This document is  on how to create Github token and store the token in HashiCorp vault which internally uses the token as part of pipeline.

## Prerequistes 
- User required to have email to activate the account.
- Windows - You can download Cygwin from cygwin.com or GitBash from git-scm.com/downloads.

## Summary ##

#### Generating the new keys
#### GitHub Account creation
#### Set up SSH keys
#### Create the token
#### Add user and token to the repositories
#### Configure on HashiCorp Vault
#### Integrate with Pipeline

## ##



### Generating the new keys

   Enter the command to generate the SSH key. 

   The following command will create a new key with GitHub email address:
	
   Eg: ssh-keygen -t rsa -b 4096 -C "email@example.com"
	
   An SSH key is a encrypted key pair that authenticates identity. 

#### Create a passphrase 

   This adds an additional layer of security to your key, as unknown users will need to enter the passphrase before the key will work.
  
   You'll be prompted to confirm the passphrase when creating it.
  
   Copy the SSH key contents to your clipboard. 
  
   Once the key has been created, you'll need to add it to your repository.
  
	
   The following command will copy the contents of the key to your clipboard

   Eg:	
  
   Windows - clip < ~/.ssh/id_rsa.pub
	
   Mac - pbcopy < ~/.ssh/id_rsa.pub

## ##
### GitHub Account creation
			
   Log into the GitHub website or register on github for machine account. 
	
   Click your profile image in the upper-right corner and select "Your profile." This will open your GitHub profile page.
  
	
   ![](./images/user-sign.PNG)

## ##
### Set up SSH keys

   Click your profile image in the upper-right corner and select "Settings." This shows left side of profile  "SSH and GPG keys".
  
   Click on "SSH and GPG keys" then edit "New SSH key"
	
   ![](./images/add-ssh-keys.PNG)

## ##
### Create the token

   Click your profile image in the upper-right corner and select "Settings." This shows left side of profile  "Developer settings".
  
   Click on "Developer settings" then click on  "Personal access tokens" then click on "Generate new token"
	
   Create Note, Expiration the token and select the scopes for what level of access required.
  
   This token is used for auto authentication. 
   
   Note: Please select token expiry days as per MoD security policy.
  

   ![](./images/generate-token.PNG)

## ##
### Add user and token to the repositories

#### Adding the Key to Your Repository

   Make sure you log in with an account that can access the repository.
  
   Click your profile image in the upper-right corner and select "Your profile." This will open your GitHub profile page.
  
     
   Click the "Repositories" tab. This will display all of your repositories.
  
   Select the repository you want to add the key to.
  
   ![](./images/add-deploy-keys.PNG) 
     
   Click the "Settings" tab at the top of the screen. This will open your repository settings.
  
     
   Click the "Deploy keys" button in the left menu
  
   ![](./images/add-deploy-keys2.PNG) 
     
   Click the "Add deploy key" button. A text field for the key will appear.
     
   ![](./images/add-new-deploy-keys.PNG) 
   
   Paste the copied deploy key into the field.


#### Adding the users to the Repository
     
   Open the first repository you want to give the machine user access to. You can find your repositories in the "Repositories" tab on your Profile page.
      
   Click the "Settings" tab on the repository page. This will display the repository settings.
  
    
   Click the "Collaborators" option in the left menu. This will allow you to add collaborators to the repository.
  
   ![](./images/add-user-to-repo.PNG) 
     
   Enter the machine user's name and click "Add collaborator." The machine user will be given read/write access to the repository
  
   ![](./images/add-new-user-to-repo.PNG) 
     
     
 
## ##
## Configure on HashiCorp Vault

   Configure github user token on vault such way that can be utilised in pipeline builds and update the manifest on github.
 
   login to vault and select the namespace. As per screenshot dso namespace is used for dso team , This differs based on team.
 
   Please refer on creating the namespace : https://github.com/defencedigital/dso-scm/blob/main/Onboarding-Docs/VaultAdminOnboarding.md
   
   Select "Secrets" and click on kv then select secret name
 
 
   ![](./images/vault-update.PNG)

## ##
##  Integrate with Pipeline 

   Update the vault-git-clone.yaml and vault-git-update-deployment.yaml files which resides under  <path>\common\ClusterTask folder.
	
   Note: These are cluster tasks so functionality will impacts in other pipelines if this is being used.

    Eg:
    - default: pipeline-github
      name: vaultRole
      type: string
    - default: dso
      name: vaultNamespace
      type: string
    - default: kv/data/github
      name: vaultPath
      type: string
 
	
### Validate
	
	
   Run the pipelines and make sure builds and uploading images / updating the manifests works as expected.
## ##
