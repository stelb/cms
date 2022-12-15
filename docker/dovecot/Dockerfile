FROM alpine:latest

LABEL maintainer="tag+dockerimage@stelb.de"

ENV LC_ALL C

RUN apk add dovecot dovecot-mysql \
	dovecot-ldap dovecot-lmtpd \
	dovecot-gssapi dovecot-pigeonhole-plugin dovecot-lua \
	dovecot-pigeonhole-plugin-ldap dovecot-pgsql \
	dovecot-submissiond dovecot-pop3d \
	tini && \
	addgroup -g 1000 vmail && \
	adduser -u 1000 -G vmail vmail -h /srv/vmail -D && \
	mkdir /srv/mail && \
	chown vmail:vmail /srv/mail && \
	rm -rf /etc/dovecot && \
	mkdir -p /etc/dovecot/conf.d

ADD dovecot.conf /etc/dovecot/dovecot.conf
ADD 00_default.conf /etc/dovecot/conf.d/00_default.conf

# lmtp, imap, imaps, pop3, pop3s, submission, managesieve
EXPOSE 24 143 993 110 995 587 4190

VOLUME ["/etc/dovecot", "/etc/dovecot/conf.d", "/srv/mail"]

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/usr/sbin/dovecot", "-F"]
