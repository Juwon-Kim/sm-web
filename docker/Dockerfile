jenkins@jenkins:/usr/share$ exit
exit
juwon-admin@juwon-nas:/volume1/docker/nginx/sm-nginx$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS         PORTS                                                          NAMES
18df5541286a   jenkins/jenkins:lts    "/usr/bin/tini -- /u…"   14 seconds ago   Up 5 seconds   0.0.0.0:50000->50000/tcp, 8080/tcp, 0.0.0.0:58080->58080/tcp   jenkins
7a942f0bde43   nginx:latest           "/docker-entrypoint.…"   22 hours ago     Up 2 hours     0.0.0.0:9080->80/tcp, 0.0.0.0:9443->443/tcp                    sm-nginx
f0011bbcf3b2   jboss/wildfly:latest   "/opt/jboss/wildfly/…"   2 days ago       Up 2 hours     0.0.0.0:18080->8080/tcp, 0.0.0.0:19990->9990/tcp               sm-wildfly
juwon-admin@juwon-nas:/volume1/docker/nginx/sm-nginx$ docker exec -it jenkins /bin/bash
jenkins@jenkins:/$ ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
jenkins@jenkins:/$ cat /var/jenkins_home/secrets/initialAdminPassword 
df95fe6ed60b47b1828ee8c8bc752a22
jenkins@jenkins:/$ ipconfig
bash: ipconfig: command not found
jenkins@jenkins:/$ ifconfig
bash: ifconfig: command not found
jenkins@jenkins:/$ client_loop: send disconnect: Broken pipe
juwonk@gimjuwon-ui-MacBookPro Documents % ssh -p 8022 juwon-admin@192.168.55.44
juwon-admin@192.168.55.44's password: 

Synology strongly advises you not to run commands as the root user, who has
the highest privileges on the system. Doing so may cause major damages
to the system. Please note that if you choose to proceed, all consequences are
at your own risk.

Could not chdir to home directory /var/services/homes/juwon-admin: No such file or directory
juwon-admin@juwon-nas:/$ clear











juwon-admin@juwon-nas:/$ ls
bin   checksum.syno  dev       etc           initrd  lib32  lost+found  opt   root  sbin             sys  tmpRoot  var           volume1
boot  config         dump.rdb  etc.defaults  lib     lib64  mnt         proc  run   SynoUpgrade.tar  tmp  usr      var.defaults
juwon-admin@juwon-nas:/$ cd /volume1/
juwon-admin@juwon-nas:/volume1$ ls
@appconf  @appstore       @database  @eaDir           @S2S        @SynoDrive              @SynologyApplicationService  @tmp             video
@appdata  @apptemp        docker     miracle-morning  @sharesnap  @SynoFinder-etc-volume  @synologydrive               @USBCopy         @webdav
@apphome  @config_backup  @docker    music            @synoconfd  @SynoFinder-log         @SynologyDriveShareSync      @userpreference
juwon-admin@juwon-nas:/volume1$ cd docker/nginx
juwon-admin@juwon-nas:/volume1/docker/nginx$ ls
sm-nginx
juwon-admin@juwon-nas:/volume1/docker/nginx$ cd sm-nginx/
juwon-admin@juwon-nas:/volume1/docker/nginx/sm-nginx$ ls
default.conf  Dockerfile  nginx.conf
juwon-admin@juwon-nas:/volume1/docker/nginx/sm-nginx$ vi Dockerfile
juwon-admin@juwon-nas:/volume1/docker/nginx/sm-nginx$ vi Dockerfile


























#nginx 이미지를 사용합니다. 뒤에 tag가 없으면 latest 를 사용합니다.
FROM nginx

# root 에 app 폴더를 생성
RUN mkdir /opt/app

# work dir 고정
WORKDIR /etc/nginx

# work dir 에 build 폴더 생성 /etc/nginx/build
RUN mkdir ./build

# host pc의 현재경로의 build 폴더를 workdir 의 build 폴더로 복사

# ADD ./build ./build


# git & vi  명령어 설치 & git clone
RUN apt-get update && apt-get install -y git \
    && apt-get install -y vim \
    && git clone https://github.com/Juwon-Kim/sm-web.git /opt/app \
    && rm /etc/nginx/conf.d/default.conf \
    && rm /etc/nginx/nginx.conf

# git과 npm은 jenkins가 설치된 Host에서 진행할 예정이라 아래 코드는 임시
RUN apt-get install -y npm \
    && npm install \
    && npm run build



# host pc 의 nginx.conf 를 아래 경로에 복사
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./default.conf /etc/nginx/conf.d/default.conf


# 80 포트 오픈
EXPOSE 80

# container 실행 시 자동으로 실행할 command. nginx 시작함
CMD ["nginx", "-g", "daemon off;"]
"Dockerfile" 41L, 1065B                                                                                                                       1,1           All
