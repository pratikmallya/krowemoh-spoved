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

#### app_a

```
podman run -p 127.0.0.1:8080:5000/tcp localhost/local-registry/app-a:latest
```

#### app_b

```
podman run -p 127.0.0.1:8081:5001/tcp localhost/local-registry/app-b:latest
```

### Test

#### app_a

```
❯ curl 127.0.0.1:8080/hello
Hello there⏎
```

#### app_b

```
❯ curl -X POST -d 'token=mytoken' http://127.0.0.1:8081/auth
density⏎
```