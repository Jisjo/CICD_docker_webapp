# CICD_docker_webapp
CI/CD using Jenkins. Building and Deploying docker container using Ansible. 

Installing Jenkins

```
amazon-linux-extras install epel -y
yum install java-1.8.0-openjdk-devel -y
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum -y install jenkins
systemctl start jenkins
systemctl enable jenkins
```

![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/1.png)
```
[root@ip-172-31-13-24 ~]# cat /var/lib/jenkins/secrets/initialAdminPassword
*******
[root@ip-172-31-13-24 ~]#
```

![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/2.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/3.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/4.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/5.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/6.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/7.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/8.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/9.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/10.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/11.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/12.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/13.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/14.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/15.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/16.png)

Select Free style project

![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/17.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/18.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/19.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/20.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/21.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/22.png)


Choose advanced >> Disable the host SSH key check
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/23.png)


Enable Webhooks for Repository

![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/24.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/25.png)
![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/26.png)

Error
```
TASK [Gathering Facts] *********************************************************
fatal: [172.31.13.54]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: Warning: Permanently added '172.31.13.54' (ECDSA) to the list of known hosts.\r\nno such identity: key.pem: No such file or directory\r\nPermission denied (publickey,gssapi-keyex,gssapi-with-mic).", "unreachable": true}
```
Fix
```
[root@ip-172-31-13-24 deployment]# chown jenkins /var/deployment/key.pem
[root@ip-172-31-13-24 deployment]#
```

Also make sure that you have updated full path for private key file in hosts file.

```
[root@ip-172-31-13-24 deployment]# cat hosts
[Build]
172.31.13.54 ansible_user="ec2-user" ansible_private_key_file="/var/deployment/key.pem"
[Test]
172.31.6.82 ansible_user="ec2-user" ansible_private_key_file="/var/deployment/key.pem"
[root@ip-172-31-13-24 deployment]#
```

So any time we make changes to the repo https://github.com/jisjo/Dockerizing-a-Python-web-app.git an automatic build will be started.

Result

![image](https://github.com/Jisjo/CICD_docker_webapp/blob/main/img/28.png)



