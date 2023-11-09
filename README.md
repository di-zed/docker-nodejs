# DiZed Docker Compose for the multiple Node.js projects

## Structure

**The most interesting folders:**

1. **./images** The folder with custom Docker Images.
2. **./local** Folder for local changes. It can be convenient to use it together with the docker-compose.local.yml file.
3. **./mounted** A folder for exchanging files between the PC and the Docker container.
4. **./volumes** The folder with Docker Volumes in Linux structure.
   1. **./volumes/home/projects** Node.JS projects.

## Setup

1. Copy the *./.env.sample* file to the *./.env*. Check it and edit some parameters if needed.
2. Copy the *./volumes/root/bash_history/node.sample* file to the *./volumes/root/bash_history/node* for saving command history in the Node container.
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

## Project setup

1. Copy the dir with the project to the *./volumes/home/projects/project-name* folder.
2. Add your own configurations to the project like connection to the DB, Mailcatcher, etc.
3. **Optional.** Add the configurations to the *docker-compose.local.yml* if you use it.

But **pay special attention** to **hostname** when you create a server! With docker you can have connectivity problems if you use **localhost** or **127.0.0.1**, because it refers to the docker container and not to your local machine, therefore the container will only listen for connections from inside the container itself. It's better to use use **0.0.0.0** or directly the ip associated to the container so that we can issue requests from our local machine or from other containers.

https://www.nodejsdesignpatterns.com/blog/node-js-development-with-docker-and-docker-compose/

## Debug configuration

### PhpStorm / WebStorm

PhpStorm: https://www.jetbrains.com/help/phpstorm/node-with-docker-compose.html

WebStorm: https://www.jetbrains.com/help/webstorm/node-with-docker-compose.html

The **Run/Debug Configurations** example with Nodemon:

![Run/Debug Configurations Nodemon](https://raw.githubusercontent.com/di-zed/internal-storage/main/readme/images/docker-nodejs/debug_config_nodemon.png)

## Containers

### MongoDB (7.0.2)

- Host: mongodb
- Port: 27017
- User: {see .env file}
- Password: {see .env file}

```code
docker-compose exec mongodb /bin/bash
```

### Node (18.18.0)

- Host: node18
- Port: 3000

```code
docker-compose exec node18 /bin/bash
```

### MailCatcher (0.8.2)

- Host: mailcatcher
- Port: 1025
- URL: http://localhost:1080/