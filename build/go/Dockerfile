# -----------------------------
# Build Container for local dev
# -----------------------------
FROM golang:1.17 AS builder

# Reflex for hot reloading
RUN go get -u github.com/cespare/reflex

# Install Dependencies
WORKDIR /src
COPY ./go.mod ./go.sum ./
RUN go mod download

# Install Reflex Config
COPY ./build/go/reflex.conf /
COPY . .

ARG BUILD_CMD
ENV BUILD_CMD $BUILD_CMD
WORKDIR /src/cmd/$BUILD_CMD
ENV CGO_ENABLED=0

WORKDIR /src
CMD ["reflex", "-d", "none", "-c", "/reflex.conf"]
