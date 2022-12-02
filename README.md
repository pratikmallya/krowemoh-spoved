### Build

#### app_a

```
cd app_a
podman build . -t local-registry/app-a
```

#### app_b

```
cd app_b
podman build . -t local-registry/app-b
```

### Run

Create a custom network

```
docker network create apps
```
#### app_a

```
podman run --network=apps --rm --name app-a localhost/local-registry/app-a:latest
```

#### app_b

```
podman run  --network=apps --rm --name app-b localhost/local-registry/app-b:latest
```

### Test
Create an interactive curl container:

```
podman run --rm -it  --entrypoint sh --network apps curlimages/curl
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

Using docker desktop's kubernetes engine.

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