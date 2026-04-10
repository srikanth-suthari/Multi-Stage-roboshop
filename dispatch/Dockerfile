# Stage 1
FROM golang AS build

WORKDIR /opt/server

COPY main.go .

RUN go mod init dispatch \
    go get \
    go build dispatch

# Stage 2
FROM alpine

WORKDIR /opt/server

RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server

EXPOSE 8080

ENV AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server

USER roboshop

CMD ["./dispatch"]