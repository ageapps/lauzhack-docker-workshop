# Dockerizing the application

Suposing that [`Docker`](https://www.docker.com/products/docker-desktop) is installed, this task consists on running out application in a docker container.


This time, the folloting modifications have to be made in our `app.js`:
```javascript
...
const os = require("os");
...
const hostname = os.hostname();
const port = process.env.PORT || 3000;
...
```

## Running the server
Test again the server locally:
```bash
$ node app.js
Server running at http://<your hostname>:3000/
```

## Dockerfile

Check out the base image that we're going to use in [Docker Hub](https://hub.docker.com/_/node/) .

The `Dockerfile.yml` that wraps our applications looks like this:
```yaml
FROM node:8.14.0-alpine

MAINTAINER Adrián García Espinosa "age.apps.dev@gmail.com"

# Create app directory
WORKDIR /app

# Bundle app source
COPY . /app

# EXPOSE '${PORT}'
ENV PORT 3000
EXPOSE 3000

CMD [ "node", "app.js" ]
```

## Running Container

Fist of all, let's build a container with out application called `simple-server` with the tag `v1`:
```bash
$ docker build -t simple-server:v1 .
Sending build context to Docker daemon   5.12kB
Step 1/7 : FROM node:8.14.0-alpine
...
Successfully built ffbbc2a0da1f
Successfully tagged simple-server:v1
```

Once we have our code inside a container, let's run it.
It's important to note that using option `-p` we map the container's port to a local one like `<host_port>:<app_port>`:
```bash
$ docker run -p 8080:3000 simple-server:v1
Server running at http://<container hostname>:3000/
```
To check running containers:
```bash
$ docker ps
CONTAINER ID  IMAGE             COMMAND        CREATED        STATUS        PORTS                   NAMES
81456635fe7e  simple-server:v1  "node app.js"  3 minutes ago  Up 3 minutes  0.0.0.0:8080->3000/tcp  kind_jackson
```
## Next steps

+ Create a new Dockerfile using another `Node.js` version and give it a new tag `v2`
+ Run locally 2 versions of the app with both versions of `Node.js` (use different host ports)
+ Check hostname of each container
+ Change the application port using the `-e` option
