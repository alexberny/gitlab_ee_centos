## Install Centos
## Install container group
  ```sudo yum -y install podman```
## Create gitlab directory on server
```
sudo mkdir -p ~/gitlab/{config,logs,data}
```

## Install Gitlab-EE Docker
```
podman run --detach \
  --hostname gitlab.localdomain \
   --publish 8443:443 --publish 8080:80 --publish 2222:22 \
   --name gitlab \
   --restart always \
   --volume ${PWD}/gitlab/config:/etc/gitlab:Z \
   --volume ${PWD}/gitlab/logs:/var/log/gitlab:Z \
   --volume ${PWD}/gitlab/data:/var/opt/gitlab:Z \
   gitlab/gitlab-ee:latest
```
## Generate systemd file
```
podman generate systemd --restart-policy=always -t 1 -f --name gitlab
```

### replace WantedBy directive
```
WantedBy=default.target
```

## Move file to user's systemd
```
cp container-gitlab.service ~/.config/systemd/user/container-gitlab.service
```

## Enable service
```
systemctl --user enable container-gitlab
systemctl --user daemon-reload
```

## Open ports on firewall
```
sudo firewall-cmd --permanent --zone=public --add-port=8080/tcp
sudo firewall-cmd --permanent --zone=public --add-port=8443/tcp
sudo firewall-cmd --permanent --zone=public --add-port=2222/tcp
```

## Reboot

## Post install
### Disable Sign-up
### Enalbe Ldap
