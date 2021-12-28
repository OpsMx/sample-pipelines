# Sample Pipelines

These pipeline demonstrates various samples of pipelines in spinnaker.

### AWS-Deployment Pipeline:
   This pipeline describes deployment to AWS. The image tag is parameterized and also finding the image using tag and its getting deployed to EC2 instance
   Requirements - AWS Integration need to be done with spinnaker.

### Blue-Green Pipeline:
   This sample pipelines shows blue-green kubernetes deployment. There are two seperate blue and green pipelines to demonstarate blue-green deployment.

### Blue-Green Ingress Pipeline:
   The blue-green deployment pipeline with Ingress based traffic is demonstrated in blue-ingress and green-ingress pipelines.

### Docker trigger Pipeline:
   The pipeline demonstrates how pipeline triggered and executed when the docker repo is pushed with new tag of image.
   Requirements - DockerHub Integration need to be done with spinnaker.

### Git trigger Pipeline:
   The pipeline demonstrates how pipeline triggered and executed when the Git repo is updated or pushed the latest code.
   Requirements - GitHub Integration need to be done with spinnaker.

### Helm-chart Pipeline:
   This sample pipeline shows the Kubernetes deployment through Helm chart. Bake stage fetch the helm chart from Github repo and deploy stage make uses of            produced base64 artifact from bake stage and deploys it.

### Jenkins-stage Pipeline:
   A sample pipeline which demonstrates the Jenkins stage to Build a Jenkins job and to get the required Build parameters.
   Requirements - Jenkins Integration need to be done with spinnaker.

### Jenkins-Trigger Pipeline:
   This sample pipeline shows the jenkins job will trigger the spinnaker pipelines and deploys the manifest based on properties from jenkins build.
   Requirements- Need to integrate jenkins account in spinnaker.

### Jira-Trigger Pipeline:
   This sample pipeline shows  jira trigger and deploys manifest according to the jira id states.
    Requirements- Need to integrate jira account in spinnaker.

### K8's-Deploy-Git-manifest Pipeline:
   This sample pipeline shows  kubernetes deployment by fetching the artifact from github.

### K8's-Deploy-manifest Pipeline:
   The pipeline shows the normal Kubernetes Deployment with the manifest given as text artifact.

### Kayenta-canary-analysis Pipeline:
   This pipeline shows the Kayenta canary analysis. It analysis the metrics for canary release against baseline.
    Requirements - Kayenta Integration need to be done with spinnaker and also Canary Analysis should be enabled.

### Kustomize Pipeline:
   This sample pipeline shows the deployment through Kustomization chart. Same as Helm chart pipeline.

### Policy Pipelines:
#### opa-runtime policy:
   This pipeline demonstrates the policy adherence at the execution time of pipeline.Like Enforce-blackout-window policy defines the deployment restriction on the    given duration.
#### prod-static-policy:
   This sample pipeline shows the opa static policy use case.Where the pipeline starts with prod must have Manual Judgement and Deploy stages at the time of          pipeline creation.

### opsmx-gitops application:
   GitOps is an operational paradigm that says that the target environment is in sync with a git repo. While we do not have full GitOps, the model being followed    can be extended to GitOps in future.
#### SyncToGit Pipeline:
   When we execute this pipeline will sync the halyard configuration to the git repo.
#### SyncToSpinnaker Pipeline:
   This pipeline is viceversa of previous one where the changes in the git repo will get updated in the spinnaker.
##### Restart-Halyard:
   This pipeline is used to restart the halyard pod of spinnaker. Usually when we sync or update the configuration.
##### Parent-LoopTrigger:
   This pipeline is used to run a child pipline(child-trigger) in a loop with the specified payload from the parent(Parent-LoopTrigger).
