---
layout: post
title: docker command list 
category: docker 
comments: true
description: 도커에서 사용하는 간단한 command 목록을 정리했습니다. 
tags:
    - docker
    - start!
---

매번 Docker의 개념만 읽으니 진도가 나아가질 않아서, 이번에는 command line 부터 다시 읽어보려 합니다. 쓰는 것부터 정리하다 보면 개념도 이해할 수 있지 않을까요...? 

#### Docker 명령어  

```
1. docker search $name 
2. docker pull $name:$version
3. docker images 
4. docker ps 
5. docker run $option $image $execute-file
6. docker start $name
7. docker restart $name
8. docker stop $name
9. docker attach $name
10. docker execute $name 
11. docker rm $name or $id
12. docker rmi $name:$version
```

> docker search $name 

```console
 ~$ docker search ubuntu
```

docker hub 에 올라가있는 image 를 검색할 수 있습니다. 이름과 설명, 공식여부 등을 알 수 있습니다. 

> docker pull $name:$version

```console
~$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
...
```

원하는 Image 를 docker hub 에서 내려받을 수 있습니다. 만약 version 을 입력하지 않을 경우, latest version으로 내려받게 됩니다.

> docker images  

```console
~$ docker images 
Using default tag: latest
latest: Pulling from library/ubuntu
...
```

pull 받은 docker image들을 검색하는 명령어입니다.

> docker ps 

```console
~$ docker ps  
...
```

아무런 옵션을 주지 않으면, 현재 실행중인 container 를 보여줍니다.

`-a` 는 All 을 의미하는 것으로, 전체 container를 보여줍니다.    
`-l` 은 latest 를 의미하는 것으로, 최근 실행한 container를 보여줍니다.    
`-q` 는 container 의 id 만을 보여줍니다.   

> docker run $option $image $execute-file

내려받은 image를 container 로 실행시키는 command 입니다. 


```console
~$ docker run -it --name ubuntu ubuntu /bin/bash   
...
```

`it`를 이용하여 실행된 bash shell 명령어 입출력을 확인할 수 있습니다.    
`--name` 으로 container 의 이름을 지정할 수 있습니다. 만약 입력하지 않으면, 임의의 값이 들어가게 됩니다. 

`$execute-file`은 container 를 올리면서 실행할 파일시킬 파일입니다.
일반적으로, Linux 의 기본 shell이 bash 이기에 `/bin/bash`를 입력하지 않아도 bash shell 로 등록됩니다. 

> docker start $name

docker container를 시작하는 명령으로, run 이후 exit을 실행하면 container가 `exit` 상태가 됩니다. 이때 아래 명령어를 입력하면 container가 실행됩니다.

```console
~$ docker start ubuntu   
...
```

> docker restart $name / docker stop $name

start 와 마찬가지로, docker container를 재시작/ 정지하는 명령입니다. 


> docker attach $name

start/ restart 는 run 처럼 container에 접속하는게 아닌, background 형태로 동작합니다. 
만약 start 후 내부 동작을 확인하고 싶을땐, attach 명령어를 사용하면 됩니다.

```console
~$ docker attach ubuntu   
...
```
> docker execute $name 

```console
~$ docker exec ubuntu echo "?"
```

docker에 명령어를 실행시킬 수 있습니다. 
또한 아래처럼 bash shell 에 접근할 수도 있습니다.


```console
~$ docker exec -it ubuntu /bin/bash
```

> docker rm $name 

docker container 를 삭제할 수 있습니다.

```console
~$ docker rm ubuntu
```

> docker rmi $name:$version

docker image를 삭제할 수 있습니다. 이때, version 명을 명시하지 않으면 모든 버전이 삭제되게 됩니다. 


#### 팁 

현재 Local 에 설치된 모든 container / image는 아래처럼 삭제할 수 있습니다. 

```console
~$ docker rm `docker ps -aq`
```


