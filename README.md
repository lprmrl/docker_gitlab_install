sudo apt update
sudo apt upgrade -y

sudo bash
apt install gitlab-runner -y
apt install mysql-client -y


gitlab-runner register
#  https://gitlab.com/
#  tocken  
#
#
# shell
systemctl start gitlab-runner
systemctl status gitlab-runner
























# docker_gitlab_install

sudo apt update
sudo apt install apt-transport-https
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce -y
apt install docker-compose -y
#sudo apt install docker-ce-cli
#sudo apt install containerd.io
#sudo apt install docker-compose-plugin
sudo systemctl status docker




sudo apt install mysql-client -y

sudo mkdir -p /data/docker/gitlab
cd /data/docker/gitlab
sudo nano .docker-compose.yml


# cat docker-compose.yml
version: '3.5'
services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    hostname: 10.106.65.24
    restart: unless-stopped
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        gitlab_rails['gitlab_shell_ssh_port'] = 8822
    ports:
      - "8000:80"
      - "8822:22"
    volumes:
      - /data/docker/gitlab/etc/gitlab:/etc/gitlab
      - /data/docker/gitlab/var/opt/gitlab:/var/opt/gitlab
      - /data/docker/gitlab/var/log/gitlab:/var/log/gitlab
    networks:
      - gitlab_net

  gitlab-runner:
    image: gitlab/gitlab-runner:alpine
    restart: unless-stopped
    depends_on:
      - gitlab
    volumes:
      - /data/docker/gitlab/etc/gitlab-runner:/etc/gitlab-runner
      - /data/docker/gitlab/var/run/docker.sock:/var/run/docker.sock
    networks:
      - gitlab_net

networks:
  gitlab_net:
  
  
  
  
  
sudo mkdir -p /data/docker/gitlab/var/opt/gitlab
sudo mkdir -p /data/docker/gitlab/var/log/gitlab
sudo mkdir -p /data/docker/gitlab/etc/gitlab-runner
sudo mkdir -p /data/docker/gitlab/var/run/docker.sock
  
  
  Стартуем:

sudo docker-compose -f docker-compose-deps.yml up -d



#sudo docker-compose up -d --force-recreate && docker-compose ps
Доступ к Gitlab из браузера через порт 8000 и через SSH через порт 8822 

Узнать пароль для учетки root из web-панели GitLab:
# docker exec -it gitlab_gitlab_1 grep 'Password:' /etc/gitlab/initial_root_password

 Убить все: laugh
# docker-compose stop && docker-compose rm -f 
  
  
  
