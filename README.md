### Build

#### app_a

```
podman build . -t local-registry/app-a
```

### Run

#### app_a

```
podman run -p 127.0.0.1:8080:5000/tcp localhost/local-registry/app-a:latest
```

### Test

#### app_a

```
❯ curl 127.0.0.1:8080/hello
Hello there⏎
```