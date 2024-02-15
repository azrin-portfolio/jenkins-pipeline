# 4. Jenkins installation on server (local or AWS EC2)
- Mac: https://www.jenkins.io/download/lts/macos/
```sh
# if java8 isn't installed yet
brew cask install java8

brew install jenkins-lts
brew services start jenkins-lts

# browse to http://localhost:8080
```
- Linux: https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos
```sh
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade
sudo yum install epel-release java-11-openjdk-devel
sudo amazon-linux-extras install epel
sudo yum install jenkins
sudo systemctl daemon-reload
sudo systemctl start jenkins
sudo systemctl status jenkins
```
- Amazon Linux 2: https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/
```sh
sudo yum update –y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade -y

# need this to fix "Requires: daemonize" error: https://stackoverflow.com/a/68891713/1528958
sudo amazon-linux-extras install epel -y
sudo yum update –y
sudo yum install jenkins java-1.8.0-openjdk-devel -y
sudo systemctl daemon-reload
sudo systemctl start jenkins
sudo systemctl status jenkins

# successful output
● jenkins.service - LSB: Jenkins Automation Server
   Loaded: loaded (/etc/rc.d/init.d/jenkins; bad; vendor preset: disabled)
   Active: active (running) since Sun 2021-08-29 14:58:51 UTC; 2s ago
     Docs: man:systemd-sysv-generator(8)
  Process: 4751 ExecStart=/etc/rc.d/init.d/jenkins start (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/jenkins.service
           └─4755 /etc/alternatives/java -Djava.awt.headless=true -DJENKINS_HOME=/var/lib/jenkins -jar /usr/lib/jenkins/jenkins.war --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkin...
```
- Windows: https://www.jenkins.io/doc/book/installing/windows/
- Docker: https://www.jenkins.io/doc/book/installing/docker/


# 4.1 How to fix an error installing credentials plugin v2.6
Refs:
- https://github.com/jenkinsci/plugin-installation-manager-tool#getting-started
- https://stackoverflow.com/a/14953877/1528958
- https://plugins.jenkins.io/credentials/#releases

```sh
cd ~

# download jenkins-plugin-manager
wget https://github.com/jenkinsci/plugin-installation-manager-tool/releases/download/2.11.0/jenkins-plugin-manager-2.11.0.jar

# find jenkins.war path
sudo find / -type f -name "jenkins.war"
/usr/lib/jenkins/jenkins.war

# install credentials v2.5 to current dir by specifying -d option
java -jar jenkins-plugin-manager-*.jar --war /usr/lib/jenkins/jenkins.war --plugins credentials:2.5 -d .

ls

# manually move credentials.jpi (plugin file) to /var/lib/jenkins/plugins/
cp credentials.jpi /var/lib/jenkins/plugins/

# restart Jenkins
sudo service jenkins restart
```