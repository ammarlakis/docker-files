FROM        docker:stable

MAINTAINER  Ammar Lakis <ammar.lakis@gmail.com>

ENV         GOPATH /go
ENV         SRCPATH ${GOPATH}/src/github.com/adnanh
ENV         WEBHOOK_VERSION 2.6.8

RUN         apk add --update -t build-deps curl go git libc-dev gcc libgcc && \
            curl -L -o /tmp/webhook-${WEBHOOK_VERSION}.tar.gz https://github.com/adnanh/webhook/archive/${WEBHOOK_VERSION}.tar.gz && \
            mkdir -p ${SRCPATH} && tar -xvzf /tmp/webhook-${WEBHOOK_VERSION}.tar.gz -C ${SRCPATH} && \
            mv -f ${SRCPATH}/webhook-* ${SRCPATH}/webhook && \
            cd ${SRCPATH}/webhook && go get -d && go build -o /usr/local/bin/webhook && \
            apk del --purge build-deps && \
            rm -rf /var/cache/apk/* && \
            rm -rf ${GOPATH}

RUN         curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose \
            chmod +x /usr/local/bin/docker-compose

VOLUME      /webhooks/
EXPOSE      9000

ENTRYPOINT  ["/usr/local/bin/webhook"]
CMD         ["-hooks", "/webhooks/hooks.json"]
