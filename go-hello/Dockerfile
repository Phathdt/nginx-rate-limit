FROM golang:1.15-alpine as builder
RUN apk update && apk upgrade && apk add --no-cache bash git openssh gcc g++
RUN mkdir /app
COPY . /app/
WORKDIR /app
RUN go mod download
RUN go build -o app

FROM alpine
RUN apk update && rm -rf /var/cache/apk/*
WORKDIR /app/
COPY --from=builder ./app /app/
EXPOSE 8080
ENTRYPOINT ["./app"]
