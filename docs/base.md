# docker入门

## 打包镜像

基于路径./（当前路径）打包一个镜像，镜像的名字是hello-docker，版本号是1.0.0

```shell
docker image build ./ -t hello-docker:1.0.0
```

### 执行过程

- FROM nginx：基于哪个镜像
- COPY ./index.html /usr/share/nginx/html/index.html：将宿主机中的./index.html文件复制进容器里的/usr/share/nginx/html/index.html
- EXPOSE 80：容器对外暴露80端口

### 查看镜像

使用docker images来查看本机已有的镜像

```shell
docker image build ./ -t hello-docker:1.0.0
```

## 运行容器

- 创建容器

```shell
docker container create -p 2333:80 hello-docker:1.0.0
```

- 结果

```text
4a25df8e18c65bcc68fbcb9d2a269266e4fb02ded0fe7bff58a81f461e65a8f2
```

- 运行容器

```shell
docker container start xxx # xxx 为上一条命令运行得到的结果

```

本地127.0.0.1:2333即可看见`index.html`的内容

### 查看当前运行的容器

```shell
docker container ls
```

### 进入容器内部

当容器运行后，可以通过如下命令进入容器内部：

```shell
docker container exec -it xxx /bin/bash # xxx 为容器ID
```

原理实际上是启动了容器内的/bin/bash，此时你就可以通过bash shell与容器内交互了。就像远程连接了SSH一样

## 总结

1. 写一个 `Dockerfile`
2. 使用`docker image build`来将`Dockerfile`打包成镜像
3. 使用`docker container create`来根据镜像创建一个容器
4. 使用`docker container start`来启动一个创建好的容器
