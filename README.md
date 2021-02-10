# sample-pipelines

This Sample-pipeline repo has Sample Application which has some basic sample pipelines of spinnaker.
These pipelines can be set as default sample pipelines when spinnaker is installed.

## Instructions for pipeline configurations

#### Git Artifacts and Helm chart pipelines
1. The pipelines in which the artifacts are stored in git repository we need to configure first the Github account into spinnaker
2. Instructions to integrate Github with spinnaker:
      1. Enable the GitHub artifact provider inside the halyard pod :  
      `` hal config artifact github enable ``
      2. Add an artifact account:  
        `` hal config artifact github account opsmxdemo_account --token <Token>  ``
3. For customizing the github account with other account which is already integrated with spinnaker. Then follow below instructions. In pipeline Json files, the      trigger section has github account, So these github account can be changed to your account.
  
   ```
   Sample Code Block for Github trigger:
   
   "triggers": [
    {
      "enabled": true,
      "project": "Your GitHub Organisation",
      "slug": "GitHub Project or repo name",
      "source": "github",
      "type": "git"
    }]
    OR
    "manifestArtifact": {
        "artifactAccount": "github account name",
        "id": "ID of the github artifact",
        "name": "Nmae of the maneifest file",
        "reference": "https://api.github.com/repos/$ORG/$REPO/contents/$FILEPATH/basedeploy.yml",  --- Link to the manifest yaml file in repo
        "type": "github/file",
        "version": "Branch"
      }
    ```
#### Docker Registry triggred  pipeline
 1. The pipeline here will get triggred through docker registry when new Image is pushed. 
 2. Configure the Docker registry with spinnaker:
    1. Enable the provider:  
      ``` hal config provider docker-registry enable ```
    2. Add the account:   
      `` hal config provider docker-registry account add my-docker-registry --address index.docker.io  --repositories opsmx11/terraspin --username <username> --password <password>  ``
 3. For customizing the docker registry account with other account which is already integrated with spinnaker. Then follow below instructions. In pipeline Json       files need to change docker registry details as shown below.
 ```
    Sample Code Block for DockerHub trigger:
    "triggers": [
    {
      "account": "Your Docker registry account name",
      "enabled": true,
      "organization": "Registry name",
      "registry": "index.docker.io",  ---- Kind of registry used dockerhub,gcr etc
      "repository": "Repository name",
      "type": "docker"
    }]
 ```
 ### Script Usage
1. Pre-requisite: 
     1. spinCLI has to installed and configured. Link to set it up -- https://spinnaker.io/setup/spin/
2. After configuring the spincli and Configuring the above instructions run the create-app.sh script.
     1.  ``` sh create-app.sh   ```  
NOTE: If you don't want some Pipeline to be created you can comment the particular pipeline save command in create-app.sh before executing it. 
    
    
    
