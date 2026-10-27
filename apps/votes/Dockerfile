FROM golang:1.26-alpine AS build

WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o votes .

FROM alpine:latest
WORKDIR /app
COPY --from=build /app/votes ./votes

EXPOSE 8081
CMD ["./votes"]

