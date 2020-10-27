## Install Centos
## Install podman
  ```sudo yum -y install podman```
## Create gitlab directory on server
```
sudo mkdir -p /srv/gitlab/{config,logs,data}
```
##
## Export gitlab directory in shell variable
```export GITLAB_HOME=/srv/gitlab```
## Download tample config
```sudo curl https://gitlab.com/gitlab-org/omnibus-gitlab/-/raw/master/files/gitlab-config-template/gitlab.rb.template?inline=false --output $GITLAB_HOME/config/gitlab.rb```
## Adjust config.rb 
Replace external_url with your URL
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
