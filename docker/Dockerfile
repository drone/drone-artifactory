FROM alpine:3.6 as alpine
RUN apk add -U --no-cache ca-certificates

FROM alpine:3.6
ENV GODEBUG netdns=go

COPY --from=alpine /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

# Install jfrog cli with version 1.35.5
RUN apk add --update \
    curl \
    && rm -rf /var/cache/apk/*
RUN curl -fL https://getcli.jfrog.io | sh /dev/stdin 1.35.5
RUN mv ./jfrog /usr/local/bin/
RUN chmod +x /usr/local/bin/jfrog

ADD release/linux/amd64/plugin /bin/
ENTRYPOINT ["/bin/plugin"]