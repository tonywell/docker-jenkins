## Docker Jenkins

### Quick Start

##### 1、构建镜像

构建jenkins master镜像

```
$ docker build -t tonywell/jenkins-master -f jenkins-master/Dockerfile .
```

构建java7和java8带maven和gradle镜像，用于jenkins slave

```
$ docker build -t tonywell/jenkins-java7 -f jenkins-jdk7/Dockerfile .
```

```
$ docker build -t tonywell/jenkins-java8 -f jenkins-jdk8/Dockerfile .
```

##### 2、启动集群

```
$ docker-compose up -d
```

