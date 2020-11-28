# setup

```
$ go get golang.org/x/tools/present
$ go get golang.org/x/tools/cmd/present
```



# docker build

```
$ docker build -t k8s-present:0.0.1 .
```

## run for development

```
$ docker run -v /Users/Sa2/go/src/github.com/Sa2/k8s-raspi-present:/go/src/app -it --rm -p 3999:3999 --name k8s-present k8s-present

$ present -http 0.0.0.0:3999
```

## run for production

```
$ docker run -it --rm -p 3999:3999 --name k8s-present k8s-present
```

## publish for private registry

```
$ docker build -t jupiter.local:5000/k8s-present:0.0.1 .

$ docker push jupiter.local:5000/k8s-present:0.0.1
```

ローカルで起動確認

```
$ docker run -it --rm -p 3999:3999 --name k8s-present jupiter.local:5000/k8s-present:0.0.1
```