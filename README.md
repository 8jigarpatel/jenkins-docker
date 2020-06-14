[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# 8jigarpatel/jenkins-docker

This repo is simply a clone of [4OH4/jenkins-docker](https://github.com/4OH4/jenkins-docker).


### Running the container

```
docker run -d \
--restart unless-stopped \
--name jenkins-docker \
-p 8080:8080 \
-p 50000:50000 \
-v v_jenkins_home:/var/jenkins_home \
-v /var/run/docker.sock:/var/run/docker.sock \
jigarpatel8/jenkins-docker
```

### Running the container with nginx-proxy & letsencrypt-nginx-proxy-companion (see further below for proxy & companion)
```
docker run -d \
--restart unless-stopped \
--name jenkins-docker \
-p 50000:50000 \
-v v_jenkins_home:/var/jenkins_home \
-v /var/run/docker.sock:/var/run/docker.sock \
-e "VIRTUAL_HOST=jenkins.address.com" \
-e "VIRTUAL_PORT=8080" \
-e "LETSENCRYPT_HOST=jenkins.address.com" \
-e "LETSENCRYPT_EMAIL=lets.encrypt@mail.com" \
jigarpatel8/jenkins-docker
```

### running nginx-proxy & letsencrypt-nginx-proxy-companion
```
docker run -d \
--restart unless-stopped \
--name nginx-proxy \
-p 80:80 \
-p 443:443 \
-v C:\Data\DockerData\nginx_certs:/etc/nginx/certs \
-v v_nginx-proxy-vhost:/etc/nginx/vhost.d \
-v v_nginx-proxy-html:/usr/share/nginx/html \
-v v_nginx-proxy-dhparam:/etc/nginx/dhparam \
-v /var/run/docker.sock:/tmp/docker.sock:ro \
jwilder/nginx-proxy

docker run -d \
--restart unless-stopped \
--name nginx-proxy-letsencrypt \
--volumes-from nginx-proxy \
-v /var/run/docker.sock:/var/run/docker.sock:ro \
-v C:\Data\DockerData\nginx_certs:/etc/nginx/certs:rw \
-e "DEFAULT_EMAIL=lets.encrypt@mail.com" \
jrcs/letsencrypt-nginx-proxy-companion
```
