# Docker Compose Install Guide
1. Run this command to download the latest version of Docker Compose:
```
sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
2. Apply executable permissions to the binary
```
sudo chmod +x /usr/local/bin/docker-compose
```
3. [Optional] Install [command completion] (https://docs.docker.com/compose/completion/) for the bash and zsh shell.
4. Check the installation
```
sudo docker-compose --version
```

### For full details please go to https://docs.docker.com/compose/install/#install-compose
