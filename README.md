# DiZed Docker Compose for the multiple Node.JS projects

## Structure

**The most interesting folders:**

1. **./images** The folder with custom Docker Images.
2. **./volumes** The folder with Docker Volumes in Linux structure.

## Setup

1. Copy the *./.env.sample* file to the *./.env*. Check it and edit some parameters if needed.
2. Copy the *./volumes/root/bash_history/nodejs.sample* file to the *./volumes/root/bash_history/nodejs* for saving command history in the Node containers.
3. **Optional.** Copy the *./docker-compose.local.yml.sample* file to the *./docker-compose.local.yml* and edit it, if you need some changes in the Docker configurations locally.

## Process

**Docker Build**
```code
docker-compose build
```

**Docker Up**
```code
docker-compose up -d
```

Docker Up, if you use some changes for the local environment:

```code
docker-compose -f docker-compose.yml -f docker-compose.local.yml up -d
```

**Docker Stop**
```code
docker-compose stop
```

## Containers

### Node v18

```code
docker-compose run node18 /bin/bash
```