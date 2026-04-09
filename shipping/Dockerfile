#Stage 1
FROM maven:3.9.11 AS builder

WORKDIR /opt/server

COPY pom.xml .

# this is known as copying the local src folder into /opt/server as the same src
COPY src ./src

RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar

#Stage 2
FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080

# Adding user and group to this image or container and the primary group with -G
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# Another workdir
# Here the actual application is being copied from the above builder
WORKDIR /opt/server
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"

# Copying the builder to this stage
COPY --from=builder --chown=roboshop:roboshop /opt/server/shipping.jar .

#Using the roboshop user
USER roboshop
CMD ["sh", "-c", "sleep 30 && java -jar shipping.jar"]