# 13. ADVANCED: Run Jenkins inside Jenkins Container 
- https://cloudbees.techmatrix.jp/blog/docker-ci-sloutions/

This will be the most advanced form of Jenkins setup.

There have been these architectures possible:

1. (wasting a server resoure) Jenkins-master process on a server & Jenkins-worker process runs a job on the same or other servers
2. (still wasting a jenkins-master server resource) Jenkins-master process on a server & Jenkins-worker process runs a job inside container
3. (still wasting a jenkins-master server resource even if jenkins-master is running in docker. Also not abstracted in k8s pod so not fault tolerant. Managing docker process is never for production use case) Jenkins-master container on a server & jenkins-worker container runs a job on some containers inside a docker container (DinD: Docker in Docker)

4. (can scale out easily by running many jenkins-worker pods on a server. jenkins-master pod can be K8s worker node so not wasting server resource) Jenkins-master container running inside K8s pod & jenkins-worker container inside K8s pod runs a job inside a docker container (DinD: Docker in Docker)