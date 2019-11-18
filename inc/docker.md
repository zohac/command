# Docker
## Install (Ubuntu with snap)
```bash
apt-get install snapd

snap install docker
```

## Docker-compose
### start
```bash
docker-compose up -d
```

### stop
```bash
docker-compose stop
```

### bash console
```bash
docker-compose run <image> bash
```

### rebuild image
```bash
docker-compose build <image>
```

## Docker
### bash console
```bash
docker run -it <image> /bin/bash
```

### prune
```bash
docker system prune -a
```
