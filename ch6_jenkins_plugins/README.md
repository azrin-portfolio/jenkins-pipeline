# 6. Useful Jenkins plugins
## blue ocean
## git/bitbucket 
- public repo
- private Bitbucket repo: https://www.youtube.com/watch?v=HTlAssPBKBs&list=PLzvRQMJ9HDiSaisKr7OnM4Fl7JXCDDcmt&index=14
- Integrate with BitBucket: build after each commit: https://www.youtube.com/watch?v=nNaR5Q_pIa4&list=PLzvRQMJ9HDiSaisKr7OnM4Fl7JXCDDcmt&index=4
- Integrate Jenkins with BitBucket Build Status API: https://www.youtube.com/watch?v=uu5XcU4EPzQ&list=PLzvRQMJ9HDiSaisKr7OnM4Fl7JXCDDcmt&index=6
## slack
- Integrate with Slack: https://www.youtube.com/watch?v=TWwvxn2-J7E&list=PLzvRQMJ9HDiSaisKr7OnM4Fl7JXCDDcmt&index=12
## pipeline
- https://www.youtube.com/watch?v=s73nhwYBtzE
## credentials binding
- scope: https://youtu.be/tuxO7ZXplRE?t=218
  - global (all jobs can see)
  - system (jobs and pipeline can’t see this)
  - normal ENV in job vs credential secrets (reducted benefit)
## docker pipeline plugin
- https://www.jenkins.io/doc/book/pipeline/docker/#custom-registry
- dokcer.build()
- docker.push()
- docker.withRegistry()
## AWS ECR plugin
- Pushing to ECR Using Jenkins Pipeline Plugin
- https://blog.mikesir87.io/2016/04/pushing-to-ecr-using-jenkins-pipeline-plugin/
```sh
docker.withRegistry('https://1234567890.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:demo-ecr-credentials') { docker.image('demo').push('latest') }
```
## Kubernetes plugin
- https://github.com/jenkinsci/kubernetes-plugin/blob/master/examples/dood.groovy
- DinD
## Monitor disk usage:
- https://www.youtube.com/watch?v=LMXdIE55rWo

