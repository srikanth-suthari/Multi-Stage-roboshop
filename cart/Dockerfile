<<<<<<< HEAD
FROM node:20
WORKDIR /opt/server
COPY *.js .
COPY package.json .
# This will install all the dependencies
RUN npm install


# Here our second stage stats
=======
# Stage 1
FROM node:20.19.5-alpine3.21 AS build
WORKDIR /opt/server
COPY package.json .
RUN npm install

# Stage 2
FROM node:20.19.5-alpine3.21
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL   com.project="roboshop" \
        component="cataloge" \
        created_by="Srikanth Chary"
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"

# Here we copy the build stage
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"]
>>>>>>> 357a9cb (multi-stage)
