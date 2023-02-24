# INSTALL DOCKER (COMPOSE) ON ORACLE LINUX 8

## INSTALLING DOCKER ENGINE

- Step 1: install yum-utils

```
sudo yum install -y yum-utils
```

- Step 2: add the Docker repository

```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

- Step 3: install Docker. Answer `y` for all prompts

```
sudo yum install docker-ce docker-ce-cli containerd.io
```

- Step 4: start Docker service

```
sudo systemctl start docker
```

- Step 5: run the hello-world image to make sure everything works

```
sudo docker run hello-world
```

## INSTALLING DOCKER COMPOSE

- Step 1: download Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

- Step 2: Add execution perms to the download

```
sudo chmod +x /usr/local/bin/docker-compose
```

- Step 3: we need to link to the docker-compose command

```
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

- Step 3: everything should work. Run `docker-compose --version` to confirm.