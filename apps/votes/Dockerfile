FROM golang:1.26-alpine AS build

WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o votes .

FROM scratch
WORKDIR /app
COPY --from=build /app/votes ./votes

EXPOSE 8081

USER 65532:65532
CMD ["./votes"]

