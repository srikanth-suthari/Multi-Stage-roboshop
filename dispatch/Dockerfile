# Stage 1
FROM golang:1.24-alpine AS builder

WORKDIR /opt/server

COPY main.go .

RUN go mod init dispatch && \
    go get && \
    go build dispatch

# Stage 2
FROM golang:1.24-alpine

WORKDIR /opt/server

RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server

EXPOSE 8080

ENV AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"

COPY --from=builder --chown=roboshop:roboshop /opt/server /opt/server

USER roboshop

CMD ["./dispatch"]