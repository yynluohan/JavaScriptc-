# docker 部署 #

开启一个虚拟机，在虚拟机下运行部署。(虚拟机ip若为：192.168.2.109)

1. 新建一个目录(test)
   test 目录下需要由 Dockerfile文件，dist(前端打包后的文件)。

   Dockerfile文件如下：

```
FROM daocloud.io/library/nginx:latest
COPY ./dist /usr/share/nginx/html
# 开放80端口
EXPOSE 80

STOPSIGNAL SIGTERM

# 启动nginx命令
CMD ["nginx", "-g", "daemon off;"]
```

2. docker生成一个镜像(比如镜像名为 saas),命令如下：

```
docker build -t saas .

```   

build成功之后，可使用 docker images 来查看生成的镜像

3. 运行

```
docker run -d -i --name saas1 -t -p 8081:80  saas   

```

```
其中：8081是虚拟机访问的端口
      80是Dockerfile(容器)开放的端口

```

4. 第三步成功之后，即可通过 http://192.168.2.109:8081 访问
