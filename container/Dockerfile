FROM golang:1.12.9-alpine3.10 AS builder
RUN apk add --no-cache build-base git
WORKDIR $GOPATH/src/kube-policy-advisor
COPY . $GOPATH/src/kube-policy-advisor
RUN env GO111MODULE=on GOOS=$(uname -s | tr '[:upper:]' '[:lower:]') GOARCH=amd64 go build -a

FROM alpine
RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*
COPY --from=builder /go/src/kube-policy-advisor/kube-policy-advisor /kube-policy-advisor

ENTRYPOINT ["/kube-policy-advisor"]
CMD ["inspect"]
