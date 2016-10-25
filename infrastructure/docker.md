# はじめてのDocker

## 導入

https://docs.docker.com/docker-for-mac/ からダウンロード、インストール

```
$ docker version
Client:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.7.1
 Git commit:   6f9534c
 Built:        Thu Sep  8 10:31:18 2016
 OS/Arch:      darwin/amd64

Server:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:        Thu Aug 18 17:52:38 2016
 OS/Arch:      linux/amd64

$ docker-compose version
docker-compose version 1.8.0, build f3628c7
docker-py version: 1.9.0
CPython version: 2.7.9
OpenSSL version: OpenSSL 1.0.2h  3 May 2016

$ docker-machine version
docker-machine version 0.8.1, build 41b3b25

$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c04b14da8d14: Pull complete 
Digest: sha256:0256e8a36e2070f7bf2d0b0763dbabdd67798512411de4cdcf9431a1feb60fd9
Status: Downloaded newer image for hello-world:latest
(snip)

$ docker run -d -p 80:80 --name webserver nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
(snip)

$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
f6ad11df522c        nginx               "nginx -g 'daemon off"   2 minutes ago       Up 2 minutes        0.0.0.0:80->80/tcp, 443/tcp   webserver

# IMAGEに書かれているのがイメージ名、NAMESに書かれているのがコンテナ名

# ブラウザで http://localhost/ を開くと nginx のデフォルトページが見える

$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              e43d811ce2f4        3 days ago          181.5 MB
hello-world         latest              c54a2cc56cbb        3 months ago        1.848 kB

$ docker stop webserver  # コンテナを停止
webserver
$ docker rm webserver    # コンテナを削除（ローカルにダウンロードされたイメージは保持したまま）
webserver
$ docker rmi nginx       # イメージを削除
Untagged: nginx:latest
Untagged: nginx@sha256:dedbce721065b2bcfae35d2b0690857bb6c3b4b7dd48bfe7fc7b53693731beff
Deleted: sha256:e43d811ce2f4986aa69bc8ba6c92f0789537f604d1601e0b6ec024e1c38062b4
Deleted: sha256:4ea7c4dceac2dbc035c7b66c24867a22949ac2e1f7c93336b2b4e12177a09368
Deleted: sha256:78024ac53358a9a2d4abf0738ab648b492638b2dc65d672a47bace227758795f
Deleted: sha256:f96222d75c5563900bc4dd852179b720a0885de8f7a0619ba0ac76e92542bbc8
```

ちなみにコンテナ名は、 `docker run` するときに `--name` オプションで与えると好きな名前を指定できる。
指定しなかった場合は自動的に生成される。生成規則：http://deeeet.com/writing/2014/07/15/docker-container-name/


## 自分のDockerイメージを作る

ディレクトリを作って `Dockerfile` という名前のファイルを作成する

例：

```
FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay
```

そのディレクトリで次を実行すると、Dockerfileの内容に基づいて `docker-whale` というイメージがビルドされる

```
$ docker build -t docker-whale .
```

これでローカルにイメージが生成されて、コンテナを起動できる

```
$ docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
docker-whale                   latest              e54e9689d4a8        About an hour ago   275 MB
hello-world                    latest              c54a2cc56cbb        3 months ago        1.848 kB
docker/whalesay                latest              6b362a9f73eb        17 months ago       247 MB
$ docker run docker-whale
 _______________________________________ 
/ It is easier to change the            \
| specification to fit the program than |
\ vice versa.                           /
 --------------------------------------- 
    \
     \
      \     
                    ##        .            
              ## ## ##       ==            
           ## ## ## ##      ===            
       /""""""""""""""""___/ ===        
  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~   
       \______ o          __/            
        \    \        __/             
          \____\______/   
```

Dockerfileに記述するコマンド

* FROM
  * イメージのベースとなるイメージ名
* RUN
  * 実行するコマンド
  * 必要なライブラリのインストールなど
* CMD
  * runしたときに実行するコマンド

Dockerfileの完全なリファレンスは https://docs.docker.com/engine/reference/builder/


## jupyter notebookを実行する

イメージとして Docker Hubにある `jupyter/datascience-notebook` を使う

https://github.com/jupyter/docker-stacks/blob/master/datascience-notebook/README.md を参照して

```
$ docker run -d -p 8888:8888 -v /path/to/host/dir:/home/jovyan/work jupyter/datascience-notebook   # 初回は数GBダウンロードするので時間がかかる
```

ブラウザで `http://localhost:8888/` にアクセスすると notebook が見える

ここで使われてる `docker` コマンドのオプション
* -d (--detach)
  * コンテナをバックグラウンドで動かす
* -p (--publish) host_port:container_port
  * ホスト側で `host_port` へアクセスしたら、コンテナ側の `container_port` へポートフォワーディングする
* -v (--volume) host_dir:container_dir
  * コンテナの `container_dir` に ホストの `host_dir` をマウントする
  * コンテナ内で生成したnotebookを、コンテナを終了させた後もホスト側から扱える
  * まあwebインターフェースからダウンロードできるけど…


## 自分のイメージを作ってDocker Hubにpush

https://hub.docker.com/ でアカウントを作成しておく。

```
$ docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
docker-whale                   latest              e54e9689d4a8        About an hour ago   275 MB
hello-world                    latest              c54a2cc56cbb        3 months ago        1.848 kB
docker/whalesay                latest              6b362a9f73eb        17 months ago       247 MB
$ docker tag e54e9689d4a8 tomerun/docker-whale:latest   # イメージにtagを付ける
$ docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
docker-whale                   latest              e54e9689d4a8        About an hour ago   275 MB
tomerun/docker-whale           latest              e54e9689d4a8        About an hour ago   275 MB
hello-world                    latest              c54a2cc56cbb        3 months ago        1.848 kB
docker/whalesay                latest              6b362a9f73eb        17 months ago       247 MB
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: tomerun
Password: 
Login Succeeded
$ docker push tomerun/docker-whale                     # Docker Hubへアップロード
The push refers to a repository [docker.io/tomerun/docker-whale]
4b6f580f8b9a: Pushed 
5f70bf18a086: Mounted from jupyter/datascience-notebook 
d061ee1340ec: Mounted from docker/whalesay 
d511ed9e12e1: Mounted from docker/whalesay 
091abc5148e4: Mounted from docker/whalesay 
b26122d57afa: Mounted from docker/whalesay 
37ee47034d9b: Mounted from docker/whalesay 
528c8710fd95: Mounted from docker/whalesay 
1154ba695078: Mounted from docker/whalesay 
latest: digest: sha256:d4bc8190f19bd1a94a66aab351b7e009c2f355d4a8f9c1db3923abd9145a45c4 size: 2614

$ docker rmi -f docker-whale           # ローカルのイメージを削除
$ docker rmi -f e54e9689d4a8           # 同上
$ docker pull tomerun/docker-whale     # Docker Hub からpull
$ docker run tomerun/docker-whale      # runできる
```


