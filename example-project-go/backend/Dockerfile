# Construir la imagen de Docker
# docker build -t k8s-hands-on -f Dockerfile .
# docker build -t k8s-hands-on:v2 -f Dockerfile . <- Esta es con version 2, se debe especificar tambien en el yaml

FROM golang:1.13 as builder

WORKDIR /app
COPY ./src/main.go .
RUN CGO_ENABLED=0 GOOS=linux GOPROXY=https://proxy.golang.org go build -o app ./main.go

FROM alpine:latest

WORKDIR /app
COPY --from=builder /app/app .
CMD ["./app"]