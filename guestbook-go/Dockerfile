# First stage: build the Go binary
FROM golang:1.23 as build

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source code into the container
COPY . .

# Build the Go app
RUN go build -o guestbook .

# Second stage: a very small image
FROM alpine:3.18

# Copy the binary from the first stage
COPY --from=build /app/guestbook /guestbook

# Expose port 3000 to the outside world
EXPOSE 3000

# Command to run the executable
ENTRYPOINT ["/guestbook"]
