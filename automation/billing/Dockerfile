# FROM 1.11-alpine3.7 as builder
FROM golang:1.11-alpine3.7 as builder

RUN apk add --no-cache make git bash gcc musl-dev
ENV GOCACHE=/tmp/on
ENV GO111MODULE=on

WORKDIR /go/src/my_project
COPY ./billing ./billing
RUN cd /go/src/my_project/billing && make build


FROM alpine:3.7
COPY --from=builder /go/src/my_project/billing/billing /

CMD ["/billing"]
