FROM multiarch/debian-debootstrap:armhf-buster-slim

RUN apt-get update && apt-get upgrade -y \
	&& apt-get install -y curl ca-certificates dnsutils && \
    rm -rf /var/lib/apt/lists/*


RUN ["/bin/bash", "-c", "set -o pipefail && wget -qO - https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-arm.tgz | tar xz -C ./"]
RUN chmod +x ./cloudflared

HEALTHCHECK CMD dig @127.0.0.1 -p 5053 google.com || exit 1

ENTRYPOINT ["./cloudflared"]
CMD ["proxy-dns","--port","5053","--address","0.0.0.0","--upstream","https://dns-family.adguard.com/dns-query"]
EXPOSE 5053/udp



