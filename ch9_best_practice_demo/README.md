# 9. BEST PRACTICE DEMO: Create Jenkins Job that gets triggered by private Git commit, and push 1) git tag and 2) build status back to the git commit

Refs:
- https://stackoverflow.com/a/51003334/1528958
- https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token

![alt text](../imgs/git_commit_build_status_and_git_tag.png "")



## 9.1 Create EC2 in Public Subnet (NOTE: only for demo to access Jenkins without load balancer)

## 9.2 Create Security Group and Allow Port 22 and 8080

## 9.3 Configure Jenkins Credential for ssh key so that Jenkins can pull from private Git repo

# 9.4 Install git to Jenkins server (git plugin should also be installed already)

If you try to use git without installing git, you will face an error like `GitException: could not init`:

![alt text](../imgs/git_not_installed_error.png "")


SSH into a server and install git
```sh
# after ssh into a Jenkins server
sudo yum install git -y

which git # (not needed) set this path to git path in Manage Jenkins > Global Tool Configuration > Git / Path to Git executable. https://stackoverflow.com/a/42703766/1528958
sudo service jenkins restart
```

It should look like this after installing git:
![alt text](../imgs/global_tool_config_git.png "")


## 9.5 Configure Git Webhooks to Push to Jenkins endpoint whenever a commit is pushed

![alt text](../imgs/git_webhooks.png "")


## 9.6 Configure Jenkins Job Build Trigger

![alt text](../imgs/jenkins_job_build_trigger.png "")

## 9.7 Generic job that prints out job name and build name

```sh
echo "First Build!"
echo "${JOB_NAME} - #${BUILD_NUMBER}"
```

## 9.8 Configure Git Publisher to push tags to git commit

![alt text](../imgs/git_publisher.png "")


## 9.9 Commit something to test if git triggers Jenkins build automatically

![alt text](../imgs/git_webhook_job_logs.png "")

Check git tag is added to the Git commit:
![alt text](../imgs/git_publisher2.png "")


## 9.10 Configure Github Commit Status (universal) on Jenkins Job
![alt text](../imgs/git_commit_status_jenkins_setting.png "")


## 9.11. Generate Git's Personal Access Token (password) for Jenkins to get authenticated to Git

![alt text](../imgs/git_generate_access_token_for_jenkins1.png "")
![alt text](../imgs/git_generate_access_token_for_jenkins2.png "")
![alt text](../imgs/git_generate_access_token_for_jenkins3.png "")
![alt text](../imgs/git_generate_access_token_for_jenkins4.png "")


## 9.12 Configure Git server on Manage Jenkins > Configure System
![alt text](../imgs/github_server_config1.png "")
![alt text](../imgs/github_server_config2_credential_secret_text.png "")
![alt text](../imgs/github_server_config3_test_connection.png "")


## 9.13 Check Git Commit has build status icon
![alt text](../imgs/git_commit_with_build_status1.png "")
![alt text](../imgs/git_commit_with_build_status2.png "")

