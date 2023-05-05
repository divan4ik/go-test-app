FROM golang:1.20 as builder

ENV CGO_ENABLED=0\
    GOOS=linux \
    GOARCH=amd64 \
    GOSUMDB=off

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
RUN go mod download
COPY . .
RUN go build -a -installsuffix cgo -o test-app main.go

FROM scratch
COPY --from=builder /app/test-app .
EXPOSE 8080
ENTRYPOINT ["./test-app"]