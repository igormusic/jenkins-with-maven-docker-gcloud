# Jenkins docker setup

This Docker image will add following to base jenkins/jenkins:lts image:

- maven - allows running mvn from command line
- nano - simple terminal text editor
- sudo - run as root
- docker - allows Jenkins to build docker images (for example Spotify dockerfile-maven-plugin )
- gcloud command line - publish docker images to Google Cloud registry

For docker build to work in Jenkins your host needs to have docker installed on your host (see /var/run/docker.sock:/var/run/docker.sock parameter )

Note that Jenkins runs as root (not a good practice) since I did not figure out how to give jenkins user permission to access /var/run/docker.sock

Timezone is changed to America/Toronto from UTC.

To run local instance of Jenkins docker:

```bash
docker run --name build-server  -p 8081:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock trules_jenkins
```

Docker image will be mapped to local volume jenkins_home.

You can access Jenkins from: [http://localhost:8081/](http://localhost:8081/)

When you run first time, you will need to setup Jenkins user name and password. 

To configure access from Jenkins to Google cloud run in docker instance shell:
```bash
 gcloud auth login
 gcloud config set project transact-rules-dev
```

