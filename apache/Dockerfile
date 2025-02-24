FROM registry.suse.com/suse/sle15:15.6
LABEL maintainer="Michele Bologna <michele.bologna@suse.com>"
LABEL name="SUSE Manager apache build profile"
LABEL version="3.0.2-20250224"

ARG repo
ARG cert

RUN echo "$cert" > /etc/pki/trust/anchors/RHN-ORG-TRUSTED-SSL-CERT.pem
RUN update-ca-certificates
RUN echo "$repo" > /etc/zypp/repos.d/susemanager:dockerbuild.repo

RUN zypper --non-interactive in aaa_base aaa_base-extras net-tools timezone vim less sudo tar python apache2 apache2-prefork

ADD pub.conf /etc/apache2/conf.d/pub.conf
RUN mkdir -p /srv/www/htdocs/pub/
ADD index.html /srv/www/htdocs/pub/index.html

CMD /usr/sbin/start_apache2 -DFOREGROUND -k start
