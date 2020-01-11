# https://pkgs.alpinelinux.org/packages?name=rsyslog*&branch=v3.11&arch=x86_64
FROM   alpine:3.11.2
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
       rsyslog-relp \
       rsyslog-imdocker \
       rsyslog-hiredis \
       rsyslog-rabbitmq
#       rsyslog-http \
#       rsyslog-snmp
RUN    adduser -s /bin/ash -D rsyslog rsyslog \
       && echo "rsyslog ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

VOLUME /config /work /logs

ENTRYPOINT ["/home/ws/starter.sh"]
CMD        ["rsyslog"]

COPY    rsyslog.conf /etc/rsyslog.conf
COPY    rsyslog.conf.d/*.conf /etc/rsyslog.conf.d/
# do end build base system

WORKDIR /home/ws
COPY    starter.sh CONTAINER.* /home/ws/
COPY    internal/* /home/ws/internal/
COPY    tools/* /home/ws/tools/
RUN     echo "`date +%F` (`date +%s`)" > /home/ws/CONTAINER.release \
        && chown -R rsyslog:rsyslog /home/ws/*
