# Dockerfile for Order Service
FROM golang:1.12-alpine AS build

#RUN apk add --update --no-cache git gcc build-base
RUN apk add --no-cache git

WORKDIR /src/
COPY main*.go go.* /src/

# update all modules listed in go.mod
#RUN go get -u
# adds any missing imported modules and remove unnecessary ones
RUN go mod tidy

RUN CGO_ENABLED=0 go build -o /bin/order-service

FROM scratch
COPY --from=build /bin/order-service /bin/order-service

EXPOSE 8001
ENTRYPOINT ["/bin/order-service"]
