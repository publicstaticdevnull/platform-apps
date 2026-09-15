 platform-apps
## What
A Postgresql database server

### [echo-server](https://artifacthub.io/packages/helm/echo-server/echo-server)
First of all. Let's add the echo-server repo. This is, in order, to download the tar.gz. Why download?, because I'm pretending **because of a security requirement, we cannot use external apps**.

This part must be done using a pipeline.
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm search repo bitnami/postgresql
helm pull bitnami/postgresql -d ../
helm repo index ../
```
Now, push the changes and next step, add the **platform-apps** repo as a Helm chart repo. Pretending you are on **echo-server** folder.

```bash
helm repo add platform-apps https://publicstaticdevnull.github.io/platform-apps
helm search repo platform-apps
helm install postgresql platform-apps/echo-server \
--create-namespace=true \
--namespace=platform-apps \
-f values.yaml
```
## To Do
1. Github actions to check security on Helm charts tar.gz
2. Github actions to test any change on the helm chart
