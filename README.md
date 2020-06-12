[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# 8jigarpatel/jenkins-docker

This repo is simply a clone of [4OH4/jenkins-docker](https://github.com/4OH4/jenkins-docker).


### Running the container

```
docker run -it -p 8080:8080 -p 50000:50000 \
    -v jenkins_home:/var/jenkins_home \
    -v /var/run/docker.sock:/var/run/docker.sock \
    --restart unless-stopped \
    jigarpatel8/jenkins-docker
```
