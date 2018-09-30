Assignment

git clone https://github.com/zeineldin/Java-testapp.git
mv  Java-testapp Java-testapp1
cp -r Java-testapp1/ Java-testapp2
vi /assignment1/Java-testapp2/src/main/java/HelloWorld.java
vi /assignment1/Java-testapp1/src/main/java/HelloWorld.java
docker build -t java-app1 .
docker tag java-app1 abdelrahmanessameldin/java-app1
docker login
docker push  abdelrahmanessameldin/java-app1
--
Docker file :----

FROM nginx
COPY ./default.conf /etc/nginx/conf.d
EXPOSE 80

default.conf fiel:-----

server {
    listen       80;
    server_name  nginxserver;

    location /app1 {
         proxy_pass http://app1:8080/devopsarea-1.0/;
    }
    
    
      location /app2 {
         proxy_pass http://app2:8080/devopsarea-1.0/;
    }
    
    location /news {
         proxy_pass http://bbc.com/;
    }

# you could also make it with directory path like the following 
#  location / {
#        root   /usr/share/nginx/html/project;
#        index  index.html index.htm;


    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

}
----
docker build -t reverse-proxy .
docker tag reverse-proxy abdelrahmanessameldin/reverse-proxy
docker push  abdelrahmanessameldin/reverse-proxy
-----
vi docker-compose.yml
--
version: "3"
services:
  app1:
    image: abdelrahmanessameldin/java-app1
    ports:
      - "4444:8080"
    container_name: app1

  app2:
    build: ./Java-testapp2
    ports:
      - "5555:8080"
    container_name: app2

  reverse-proxy:
    image: abdelrahmanessameldin/reverse-proxy
    ports:
      - "3333:80"
    container_name: reverse-proxy
    links:
      - app1
      - app2
-----
Docker compose :--
docker-compose up -d
--------------------------------------------------------------
git init
git remote add origin  https://github.com/abdelrahmanessameldin/my-first-assignment.git
git add .
git commit -m "first commit"
git push origin master

user:abdelrahmanessameldin
pass:Sumerge@2018
