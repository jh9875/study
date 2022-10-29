도커 - 설치부터 실행까지
===

## 도커 기본 명령어

- version <br>
  도커 버전 확인

  > docker version

  설치된 도커의 버전 및 정보를 확인 가능.

  만약 다음과 같은 문구가 출력되는 경우.?
  ```Text
  Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
  ```

  도커 서버가 실행이 안된 경우. => Docker Desktop을 실행시켜준다.

- run & exec <br>
  도커 컨테이너 실행 명령어. <br>
  도커 컨테이너를 실행시키는 명령어지만 이미지가 없다면 다운로드하고 컨테이너를 실행시킨다.

  > docker run [Options] IMANGE [Command] [Args]

  주요 옵션 : 
  - -d : detached mode 컨테이너 실행시 백그라운드로 실행하게 해준다.
  - -p : 호스트와 컨테이너의 포트를 연결.
  - -v : 호스트와 컨테이너의 디렉토리를 연결.
  - -e : 컨테이너에서 사용할 환경변수 설정.
  - --name : 컨테이너 이름 설정.
  - --rm : 프로세스 종료시 컨테이너 제거.
  - -it : i옵션과 t옵션을 동시에 사용한 것으로 주로 터미널 입력을 위해 사용됨.
  - --network : 컨테이너 실행시 네트워크 연결할 때 사용.

  예제 :
  - ubuntu 20.04 컨테이너 만들고 실행. <br>
    > docker run --rm -it ubuntu:20.04 /bin/sh

    리눅스 내부에 들어가기 위해서 -it 명령을 이용하여 /bin/sh를 실행시켜 줘야함. <br>
    그리고 --rm 명령을 사용하여 컨테이너 종료시 자동으로 삭제되도록.

  - Centos8 실행 <br>
    > docker run --rm -it centos:8 /bin/sh

    ubuntu와 마찬가지로 컨테이너 이름과 : 뒤에 버전을 명시하고, -it 로 /bin/sh를 실행시켜줘서 실행.

  - Redis 실행 <br>
    > docker run --rm -p 1234:6379 redis

    실행 후 telnet으로 1234 포트 접속하면 가능.

  - mysql 실행 <br>
    > docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql

    위 명령어에선 -d 옵션으로 백그라운드에서 실행하므로 exec 명령어로 접속이 필요. 그리고 3306 포트로 접속.

    > docker exec -it mysql mysql

  - -v 옵션 사용하기. <br>
    > docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --network=app-network \
  --name mysql \
  -v /my/own/datadir/mysql:/var/lib/mysql \
  mysql

- ps <br>
  실행중인 컨테이너 확인 명령어

  > docker ps

  실행중이지 않은 컨테이너도 하려면 -a 옵션을 붙이면 됨.

  > docker ps -a

- stop <br>
  실행중인 컨테이너를 중지하는 명령어.

  > docker stop [container id .. (하나 이상 가능)]

- rm <br>
  종료된 컨테이저 제거.

  > docker rm [container id ..]

- logs <br>
  컨테이너 로그 확인

  > docker logs [container id]

- images <br>
  도커가 다운로드 한 이미지 확인.

  > docker images

- pull <br>
  도커로 이미지 다운 받기.

  > docker pull [이미지 이름]

- rmi <br>
  도커 이미지 제거.

  > docker rmi [이미지 id]

- network <br>  
  도커 컨테이너를 연결할 네트워크 생성.

  > docker network create [네트워크 이름]

  컨테이너를 네트워크에 연결하려면 connect 명령어를 사용.

  > docker network connect [네트워크 이름] [컨테이너 이름]

  또는 도커에 네트워크를 조회하려면 ls 명령 사용.

  > docker network ls

## 도커 컴포즈

