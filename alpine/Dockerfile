# https://pkgs.alpinelinux.org/packages?name=rsyslog*&branch=v3.11&arch=x86_64
FROM   alpine:3.11
LABEL  maintainer="alpinelinux@suisrc.com"
RUN    apk add --no-cache \
       rsyslog \
       rsyslog-mmdblookup \
       rsyslog-mmfields \
       rsyslog-mmjsonparse \
       rsyslog-mmnormalize \
       rsyslog-mmpstrucdata \
       rsyslog-mmrm1stspace \
       rsyslog-mmutf8fix \
       rsyslog-elasticsearch \
       rsyslog-uxsock \
       rsyslog-imdocker
#       rsyslog-http \
#       rsyslog-hiredis \
#       rsyslog-relp \
#       rsyslog-rabbitmq \
#       rsyslog-snmp
RUN    adduser -s /bin/ash -D rsyslog rsyslog \
       && echo "rsyslog ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

VOLUME /config /work /logs
CMD    ["rsyslog"]

ENTRYPOINT ["/home/appliance/starter.sh"]
COPY    rsyslog.conf /etc/rsyslog.conf
COPY    rsyslog.conf.d/*.conf /etc/rsyslog.conf.d/
# do end build base system

WORKDIR /home/appliance
COPY    starter.sh CONTAINER.* ./
COPY    internal/* ./internal/
COPY    tools/* ./tools/
RUN     echo "`date +%F` (`date +%s`)" > CONTAINER.release \
        && chown -R rsyslog:rsyslog *
