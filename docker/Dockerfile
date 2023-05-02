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
RUN rm /etc/nginx/conf.d/default.conf \
 && rm /etc/nginx/nginx.conf

# git과 npm은 jenkins가 설치된 Host에서 진행할 예정이라 아래 코드는 임시
#RUN apt-get install -y npm \
#	&& npm install \
#	&& npm run build
	


# host pc 의 nginx.conf 를 아래 경로에 복사
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY ../dist /opt/app/dist

# 80 포트 오픈
EXPOSE 80

# container 실행 시 자동으로 실행할 command. nginx 시작함
CMD ["nginx", "-g", "daemon off;"]
