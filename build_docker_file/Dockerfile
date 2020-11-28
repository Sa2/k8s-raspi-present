FROM golang:1.15.5-alpine

WORKDIR /go/src/app
COPY . .
RUN apk update && apk add git
RUN go get golang.org/x/tools/cmd/present
CMD ["present", "-http", "0.0.0.0:3999"]
# EXPOSE 3999