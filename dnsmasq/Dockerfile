FROM alpine:3.6
RUN apk --no-cache add dnsmasq
COPY dnsmasq.conf /etc/dnsmasq.conf
USER dnsmasq:dnsmasq
VOLUME /etc/dnsmasq.d/
EXPOSE 53 53/udp
ENTRYPOINT ["dnsmasq", "-k"]
