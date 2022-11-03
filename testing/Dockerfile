## Emacs, make this -*- mode: sh; -*-

FROM r-base:latest

LABEL org.label-schema.license="GPL-2.0" \
      org.label-schema.vcs-url="https://github.com/rocker-org/rocker" \
      maintainer="Dirk Eddelbuettel <edd@debian.org>"

## This was not needed before but we need it now
#ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
                python3-apt \
                python3-dbus \
                python3-gi \
        && install.r bspm \
        && echo "bspm::enable()" >> /etc/R/Rprofile.site \
        && echo 'APT::Install-Recommends "false";' > /etc/apt/apt.conf.d/90local-no-recommends \
        && chgrp 1000 /usr/local/lib/R/site-library \
        && install.r remotes

CMD ["bash"]
