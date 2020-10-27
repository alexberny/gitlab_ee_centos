## Install Centos
## Install podman
  ```sudo yum -y install podman```
## Create gitlab directory on server
```
sudo mkdir /srv/gitlab
```
## Export gitlab directory in shell variable
```export GITLAB_HOME=/srv/gitlab```
## Install Gitlab-EE Docker
```
podman run --detach \
  --hostname gitlab.example.com \
   --publish 443:443 --publish 80:80 --publish 22:22 \
   --name gitlab \
   --restart always \
   --volume $GITLAB_HOME/config:/etc/gitlab:Z \
   --volume $GITLAB_HOME/logs:/var/log/gitlab:Z \
   --volume $GITLAB_HOME/data:/var/opt/gitlab:Z \
   gitlab/gitlab-ee:latest
```
