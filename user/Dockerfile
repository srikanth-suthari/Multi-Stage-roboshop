#Stage - 1
FROM node:20.19.5-alpine3.21 AS build

#Setting a workdir
WORKDIR /opt/server

#Copying the dependency file
COPY package.json .

#Copying the app logic or application code
COPY *.js .

#Installing the depencies of the application
RUN npm install

# Stage - 2
# here node:20.19.5-alpine3.21 is an operating system with node runtime
FROM node:20.19.5-alpine3.21

#Setting a work directory
WORKDIR /opt/server

#Adding a user/group with flag -S and adding that user to its primary group with -G flag in a single layer or instruction
RUN addgroup -S roboshop && addgroup -S roboshop -G roboshop \

    #changing the permissions to the /opt/server recurcively from root to roboshop
    chown -R roboshop:roboshop /opt/server

EXPOSE 8080

LABEL   com.project="roboshop" \
        component="cataloge" \
        created_by="Srikanth Chary"

# Environment Veriables
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"

#Copying the build file from the stage 1 to here
#It comes with the dependencies and application code
COPy --from=build --chown=roboshop:roboshop /opt/server /opt/server
#Changing the permissions for /opt/server from root user to roboshop user

#Running the application with roboshop user
USER roboshop

#finally running the application
CMD ["server.js"]

#Default command when the container starts
ENTRYPOINT ["node"]