# setup

```
$ go get golang.org/x/tools/present
$ go get golang.org/x/tools/cmd/present
```



# docker build

jupiter jazz (k8sクラスタ)　で動かす場合はarmプロセッサ上でビルドする
アーキテクチャが違うのはやっぱり痛い

```
$ docker build -t k8s-present:0.0.1 .
```

## run for development

```
$ docker run -v /Users/Sa2/go/src/github.com/Sa2/k8s-raspi-present:/go/src/app -it --rm -p 3999:3999 --name k8s-present k8s-present:0.0.1

$ present -http 0.0.0.0:3999
```

## run for production

```
$ docker run -it --rm -p 3999:3999 --name k8s-present k8s-present
```

## publish for private registry

```
$ docker build -t jupiter.local:5000/k8s-present:0.0.2 .

$ docker push jupiter.local:5000/k8s-present:0.0.2

$ kubectl apply -f k8s-deployment.yaml
```

ローカルで起動確認

```
$ docker run -it --rm -p 3999:3999 --name k8s-present jupiter.local:5000/k8s-present:0.0.1
```



# tag 削除


# registryの中身確認


```
$ curl 192.168.100.161:5000/v2/_catalog
```

```
# 対象のタグリスト取得
$ curl http://192.168.100.161:5000/v2/k8s-present/tags/list
```

tag削除の例

```
$ digest=$(curl -H "Accept: application/vnd.docker.distribution.manifest.v2+json" -sI http://192.168.100.161:5000/v2/k8s-present/manifests/0.0.1 | grep Docker-Content-Digest | tr '\r\n' ' ' | awk '{print $NF}')


$ curl -X DELETE "http://192.168.100.161:5000/v2/k8s-present/manifests/$digest"
```