# -------- Stage 1: Build --------
FROM golang:1.24.4 AS builder

WORKDIR /app

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o server .

# -------- Stage 2: Runtime --------
FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/server .
COPY configs/.env /app/.env

RUN chmod +x server

ENV GOFR_ENV_FILE=/app/.env

CMD ["./server"]
