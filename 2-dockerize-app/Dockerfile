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
