# stage 1: build
FROM golang:1.20 AS build

WORKDIR /app

COPY go.mod ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o app .

# stage 2: run
FROM alpine:latest

WORKDIR /root/

COPY --from=build /app/app .

EXPOSE 8080

CMD ["./app"]