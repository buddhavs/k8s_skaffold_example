# FROM 1.11-alpine3.7 as builder
FROM golang:1.11-alpine3.7 as builder

RUN apk add --no-cache make git bash gcc musl-dev
ENV GOCACHE=/tmp/on
ENV GO111MODULE=on

# install go-swagger
RUN mkdir -p /go/src/github.com/go-swagger && cd /go/src/github.com/go-swagger && \
git clone -b 0.13.0 --depth 1 https://github.com/go-swagger/go-swagger && \
cd go-swagger/cmd/swagger && go install

WORKDIR /go/src/my_project
COPY ./api ./api
RUN cd /go/src/my_project/api && make build || true \
make build

FROM alpine:3.7
COPY --from=builder /go/src/my_project/api/api /

ENTRYPOINT ["/api"]
