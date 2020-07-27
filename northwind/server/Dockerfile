# the environment : This image will be based on Node v14
FROM node:14

## building the image
# environment variable to define my workspace
ENV APP_DIR=/app APP_PORT=3000 DB_USER=root DB_PASSWORD=changeit

# create and cd into APP_DIR
# mkdir $APP_DIR
# cd $APP_DIR
WORKDIR ${APP_DIR}

# copy the file from fortune into /app
# ADD local image
ADD main.js .
ADD package.json .
ADD package-lock.json .
# copy the directories
ADD public public
ADD views views
ADD config config

# install the dependencies - package.json
RUN npm install

# Add health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1

## running the image
# the port the application is exposing
EXPOSE ${APP_PORT}

# run the application
ENTRYPOINT [ "node","main.js" ]
