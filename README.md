### Build

#### app_a

```
podman build . -t local-registry/app-a
```

### Run

```
podman run -p 127.0.0.1:8080:5000/tcp localhost/local-registry/app-a:latest
```