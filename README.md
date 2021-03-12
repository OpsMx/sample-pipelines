# sample-pipelines

This Sample-pipeline repo has Sample Application which has some basic sample pipelines of spinnaker.
These pipelines can be set as default sample pipelines when spinnaker is installed.

## Instructions for pipeline configurations

#### Github Account Integration (Git artifact pipelines,Helm chart pipeline,blue-green deploy pipelines)
1. The pipelines in which the artifacts are stored in git repository we need to configure first the Github account into spinnaker
2. Instructions to integrate Github with spinnaker:
      1. Enable the GitHub artifact provider inside the halyard pod :  
      `` hal config artifact github enable ``
      2. Add an artifact account:  
        `` hal config artifact github account add opsmxdemo_account   ``
        (Note: If you use private repo then add the token flag for authentication `` --token <Token> `` )
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
      `` hal config provider docker-registry account add my-docker-registry --address index.docker.io  --repositories opsmx11/terraspin --username <username>  ``
        (Note: If you use private repo then add the password flag for authentication ``  --password <password> `` )
        
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
 #### AWS Integration 
  1. AWS Integration is required for aws-deploy pipeline execution. 
  2. Follow the steps given in this link---- https://www.opsmx.com/blog/deploying-to-aws-ec2-using-spinnaker/ 
        1. Setting up IAM Roles for Spinnaker pipeline Deployment
        2. AWS Integration via Halyard in spinnaker
        3. To configure Subnets and create Security Groups for Firewall Control in Spinnaker.
        4. Creating a Load Balancer in Spinnaker.
  3. After completing the above steps,need to configure some changes in pipeline as shown below:
      1. Change Account details,Looad Balancer,Firewall and required details in spinnaker UI
     
      ![AWS Deploy configuration](https://github.com/Opsmx/sample-pipelines/raw/main/screenshot/aws.png?raw=true)
  
  #### Kayenta Canary analysis pipeline
   Kayenta is the Automated Canary analysis tool that integrates tightly with Spinnaker and uses the performance metrics from APM tools to make Canary                judgement whether the release is fit for production or it needs to be rolled back.
   1. Follow the below link for step by step Integration and configuration.
      https://www.opsmx.com/blog/how-to-integrate-kayenta-with-spinnaker-for-automated-canary-analysis/
  
 #### Jira Demo
   1. Jira-Demo pipeline demonstrates k8's deployment based on jira-id status and trigger the pipeline too.
   2. Steps to execute the pipeline:
       1. Configure the Webhook in your JIRA with the source link which is in configuration of spinnaker pipeline. As shown below in Automated Trigger section
       
       ![jira webhook configuration](https://github.com/Opsmx/sample-pipelines/raw/main/screenshot/jira.png?raw=true)
       
       2. Add the custom stage - JIRA:Wait for state in spinnaker orca-local file.
       3. At pipeline runtime pass the parameters of jiraid and and image tag version.
 
 #### OPA pipelines
   1. There are two policy pipelines:
        1. Runtime-policy: Where the deployment is not allowed for a defined period in the policy
        2. Static-policy: where as in the pipline name has prod, then policy enforce to include Manual and Deploy stage.
   2. So to execute these pipline need to add the custom stage of Policy in spinnaker orca-local file. 
   3. For Runtime policy pipeline provide the following parameters in the Policy stage :
        1. Policy Proxy -- http://oes-sapor.<namespace>:8085
        2. Policy Path -- /v1/data/opa/pipelines/datetimeslot
        
 
 #### Kustomize pipeline
   1. Similar to Helm Chart pipeline will make use of Kustomize yaml files for deployment.(https://spinnaker.io/guides/user/kubernetes-v2/kustomize-manifests/)
   2. Before executing the pipline we need to integrate Git-repo account in Spinnaker (https://spinnaker.io/setup/artifacts/gitrepo/)
 ```
    Steps:
     1. hal config artifact gitrepo enable
     2. hal config artifact gitrepo account add opsmx_repo 
     (Note: If you use private repo then add the token flag for authentication  --token <Token>  )
``` 
   3. If you need to customize your diffrent account then integrate you git-repo as shown above and make necessary changes in pipeline json file
   ```
     "inputArtifact": {
        "account": "ACCOUNT NAME",
        "artifact": {
          "artifactAccount": "ARTIFACT ACCOUNT",
          "customKind": true,
          "id": "72fbda2b-2a4a-43a4-92a8-d8fe1bdd3983",
          "metadata": {
            "subPath": "kustomize/helloworld/base/"  ---- subpath of the yaml file
          },
          "reference": "https://github.com/OpsMx/sample-pipeline-manifest", ---- Reference link to repo
          "type": "git/repo",
          "version": "BRANCH" 
        } 
   ```
 ### Script Usage
1. Pre-requisite:
     1. spinCLI has to installed and configured. Link to set it up -- https://spinnaker.io/setup/spin/
2. After configuring the spincli and Configuring the above instructions.Follow below steps to create sample pipelines
 ```
     1. Create an empty directory
     2. git clone <the repo>
     3. chmod +x create*.sh
     4. ./createapp.sh
  ```     
NOTE: 
1. If you don't want some Pipelines to be created you can comment the particular pipeline save command in create-app.sh before executing it.
2. And also before executin the pipleines please do modify the Account and Namespace  accordingly
3. ##### FOR ALL CUSTOM STAGE : Get orca-local from: https://github.com/OpsMx/custom-stages.git
