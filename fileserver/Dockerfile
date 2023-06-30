FROM golang:1.19 AS builder

# PHASE 1: build

# set working directory for container
WORKDIR /build

COPY go.mod go.sum ./
# install deps
RUN go mod download

# copy the entirety of the project
COPY . .

ENV CGO_ENABLED=0 GOOS=linux GOARCH=amd64
RUN go build -o /api cmd/main.go

# PHASE 2: Test (later)

# PHASE 3: Deploy

FROM gcr.io/distroless/base-debian10

WORKDIR /

COPY --from=builder /api /api

EXPOSE 9090

CMD ["./api"]

