FROM andrius/asterisk

RUN apk update      && \
    apk add nano    && \
    apk add vim

EXPOSE 5060/udp 10000-10100/udp 5038/tcp

COPY pjsip.conf /etc/asterisk/pjsip.conf
COPY extensions.conf /etc/asterisk/extensions.conf
COPY manager.conf /etc/asterisk/manager.conf

CMD ["asterisk", "-vvv", "-f"]
