### Build

#### app_a

```
cd app_a
docker build . -t local-registry/app-a
```

#### app_b

```
cd app_b
docker build . -t local-registry/app-b
```

### Run

Create a custom network

```
docker network create apps
```
#### app_a

```
docker run --network=apps --rm --name app-a localhost/local-registry/app-a:latest
```

#### app_b

```
docker run  --network=apps --rm --name app-b localhost/local-registry/app-b:latest
```

### Test
Create an interactive curl container:

```
docker run --rm -it  --entrypoint sh --network apps curlimages/curl
```

Now run the example commands:

```
curl app-a:5000/hello
Hello there⏎
```

```
curl -X POST -H 'Authorization: mytoken' http://app-a:5000/jobs
Jobs:
Title: Devops
Description: Awesome
```

### Kubernetes

Using [docker desktop's](https://docs.docker.com/desktop/kubernetes/) kubernetes engine.

Deploy:

```
kubectl apply -f ./apps/app_a/kubernetes/
kubectl apply -f ./apps/app_b/kubernetes/
```

Test:
```
❯ curl http://localhost:5000/hello
Hello there⏎
```
and 

```
❯ curl -X POST -H 'Authorization: mytoken' http://localhost:5000/jobs
Jobs:
Title: Devops
Description: Awesome
```

### Continuous Delivery Plan

We would need to have at least 2 distinct components:

1. Build and then upload artifacts (container images, manifests etc.) to a remote repository (e.g. artifactory) on merge to master branch 
2. Deploy artifacts from remote repository to the production environment. This could be triggered after the previous step.

For evaluating tools to achieve this, would probably look at: 
* how popular the tool is (more popular generally means better support/operational knowledge)
* how hard is it to operate (prefer managed solutions over self hosted one where possible)

e.g. on Github, since Github Actions are easily available on the platform, would probably look at building the software artifacts using one action, and deploying using another. Alternatively some platforms provide built in support (e.g. Gitlab, GCP Cloud Build)

