 platform-apps
## What
This repository is a portfolio showcasing a PoC of my capabilities. For this reason, I do not recommend using it as-is in a production environment. I’m sure there are several areas that could be improved, particularly when it comes to deploying the solution in a cloud environment.

## Folders
Each folder is mapped to a specific Helm chart, and within that chart, to a specific version. This is because, in my environment, I have full control over the versions that are deployed. In other words, I do not allow external Helm charts to be used, which ensures that nothing outside of our control can be deployed.

For example, if a release published as an artifact contained a bug, it could become a problem.

## Important
The applications are managed using an Application CRD on [Argo](https://github.com/publicstaticdevnull/platform-gitops) 

## Applications
List of gitops Apps. 

### [echo-server](https://artifacthub.io/packages/helm/echo-server/echo-server)
First of all. Let's add the echo-server repo. This is, in order, to download the tar.gz. Why download?, because I'm pretending **because of a security requirement, we cannot use external apps**.

This part must be done using a pipeline.
```bash
helm repo add echo-server https://ealenn.github.io/charts
helm search repo echo-server/echo-server
helm pull echo-server/echo-server -d ../
helm repo index ../
```
Now, push the changes and next step, add the **platform-apps** repo as a Helm chart repo. Pretending you are on **echo-server** folder.

```bash
helm repo add platform-apps https://publicstaticdevnull.github.io/platform-apps
helm search repo platform-apps
helm install echo-server platform-apps/echo-server \
--create-namespace=true \
--namespace=platform-apps \
-f values.yml
```
## To Do
1. Github actions to check security on Helm charts tar.gz
2. Github actions to test any change on the helm chart
