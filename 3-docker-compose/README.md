# Simple deploy with docker-compose 

Suposing that `Docker` is installed, which comes with `docker-compose` natively. This task consists on a simgle deploy of the system with `docker-compose` on a local enviroment.

## Initial requirements

+ [`Docker` and `docker-compose`](https://www.docker.com/products/docker-desktop)
+ Clone [`docker-chat`](https://github.com/ageapps/docker-chat) repository
    ```bash
    git clone https://github.com/ageapps/docker-chat
    ```
    
## Setup
![basic](../art/arch_1.png)
+ __Web (app):__ [NodeJS] server containin all business logic and that [features](#features)  mentioned above. It uses the official [NodeJS image] as base image.
+ __Database (db):__ [MongoDB] database. It uses the official [MongoDB image] with an additional startup script which sets up users in order to have a securized database (using `MONGO_DB_APP_PASSWORD`, `MONGO_DB_APP_USERNAME`, `MONGO_DB_APP_DATABASE` enviroment variables).

## Steps
### Deployment
```bash
$ cd demo
$ docker-compose up -d
Creating network "dockerchat_default" with the default driver
Creating dockerchat_db_1 ...
Creating dockerchat_db_1 ... done
Creating dockerchat_app_1 ...
Creating dockerchat_app_1 ... done
# connect in your browser to <host IP>:8888
$ docker ps
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS                   PORTS                      NAMES
24a4374824bb        ageapps/docker-chat:app     "nodemon ./bin/www"      2 minutes ago       Up 2 minutes             0.0.0.0:8888->3000/tcp     dockerchat_app_1
932357d094d8        ageapps/docker-chat:mongo   "docker-entrypoint..."   2 minutes ago       Up 2 minutes (healthy)   0.0.0.0:27017->27017/tcp   dockerchat_db_1

```
### Clean Enviroment
```
# To stop the system
$ docker-compose down -v
Stopping dockerchat_app_1 ... done
Stopping dockerchat_db_1  ... done
Removing dockerchat_app_1 ... done
Removing dockerchat_db_1  ... done
Removing network dockerchat_default
```

[NodeJS image]: https://hub.docker.com/_/node/
[MongoDB image]: https://hub.docker.com/_/mongo/
[MongoDB]: https://www.mongodb.com
[mongoose]: http://mongoosejs.com/index.html
[NodeJS]: http://nodejs.org
[Docker]: https://docs.docker.com/
[docker-compose]:https://docs.docker.com/compose/compose-file/
[docker-build]:https://docs.docker.com/engine/reference/builder/
[Kubernetes]:https://kubernetes.io/
[WebSocket handshake]:https://tools.ietf.org/html/rfc6455
[WebSocket]:https://en.wikipedia.org/wiki/WebSocket
[MongoStore]:https://www.npmjs.com/package/connect-mongo
[GlusterFS]:https://www.gluster.org/
[traefik]:https://traefik.io/
[NATS]:https://nats.io/
[NATS Adapter]:https://www.npmjs.com/package/socket.io-nats
[RabbitMQ]:https://www.rabbitmq.com/
[Rabbit Adapter]:https://www.npmjs.com/package/socket.io-amqp
[Redis]:https://redis.io/
[Redis Adapter]:https://github.com/socketio/socket.io-redis
[traefik image]:https://hub.docker.com/r/_/traefik/
[SocketIO]:https://socket.io/
[Express Session]:https://github.com/expressjs/session
[NGINX Ingress Controller]: https://github.com/kubernetes/ingress-nginx
[ingress documentation]: https://github.com/kubernetes/ingress-nginx/blob/master/docs/catalog.md
