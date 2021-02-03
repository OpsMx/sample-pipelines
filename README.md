# sample-pipelines

This Sample-pipeline repo has Sample Application which has some basic sample pipelines of spinnaker.
These pipelines can be set as default sample pipelines when spinnaker is installed.

## Script Usage
1. Pre-requisite: spinCLI has to installed and configured. Link to set it up -- https://spinnaker.io/setup/spin/
2. In pipeline Json files, the trigger section has github account, So these github account can be changed to yiu account.Similary for Docker registry.
  
   ```
   Sample Code Block for Github trigger:
   "triggers": [
    {
      "enabled": true,
      "project": "Your GitHub Organisation",
      "slug": "GitHub Project or repo name",
      "source": "github",
      "type": "git"
    }
    ] 
    Sample Code Block for DockerHub trigger:
    "triggers": [
    {
      "account": "Your Docker registry account name",
      "enabled": true,
      "organization": "Registry name",
      "registry": "index.docker.io",  ---- Kind of registry used dockerhub,gcr etc
      "repository": "Repository name",
      "type": "docker"
    }
    ] ````
   
3. Change the necessary artifacts under matching artifact section.
    ```
    Sample Artifact changes for Github:
    "manifestArtifact": {
        "artifactAccount": "GitHub Account name",
        "id": "The Artifact ID",
        "name": "The name of the artifact"
        "reference": "https://api.github.com/repos/$ORG/$REPO/contents/$FILEPATH/deploy.yaml",  --- Link to the manifest yaml file in repo
        "type": "github/file"
      } ```

4. After making necessary changes in pipeline json files run the create-app.sh script.
   1. Give the file path for app and pipeline json inside  create-app.sh 
   2. ``` sh <filepath>/create-app.sh ```
   
    
