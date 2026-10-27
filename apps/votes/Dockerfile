FROM golang:1.26-alpine@sha256:a2012b4a1d1f9f7e9f44e0d39b805a901e856b1dd80b4e6ee4338db547050308 AS build

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
