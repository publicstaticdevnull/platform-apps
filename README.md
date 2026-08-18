# platform-gitops
## What
This repository is a portfolio showcasing a PoC of my capabilities. For this reason, I do not recommend using it as-is in a production environment. I’m sure there are several areas that could be improved, particularly when it comes to deploying the solution in a cloud environment.

## Folders
Each folder is mapped to a specific Helm chart, and within that chart, to a specific version. This is because, in my environment, I have full control over the versions that are deployed. In other words, I do not allow external Helm charts to be used, which ensures that nothing outside of our control can be deployed.

For example, if a release published as an artifact contained a bug, it could become a problem.

### Applications
List of gitops Apps

* **[ealenn](https://artifacthub.io/packages/helm/ealenn/echo-server)**: ArgoCD Helm chart setup to deploy continous delivery tool. To install this app:
```
cd ealenn
helm repo add ealenn https://ealenn.github.io/charts
helm search repo ealenn/echo-server
cd ealenn
helm pull ealenn/echo-server
helm repo index .
helm install echo-server echo-server-0.5.0.tgz \
--create-namespace=true \    
--namespace=platform-apps \ 
-f values.yml 
```
