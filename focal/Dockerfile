## Emacs, make this -*- mode: sh; -*-

FROM rocker/r-ubuntu:20.04

LABEL org.label-schema.license="GPL-2.0" \
      org.label-schema.vcs-url="https://github.com/rocker-org/rocker" \
      maintainer="Dirk Eddelbuettel <edd@debian.org>"

## This was not needed before but we need it now
#ENV DEBIAN_FRONTEND noninteractive

RUN add-apt-repository --yes "ppa:edd/r-4.0" \
	&& apt-get install -y --no-install-recommends \
                r-cran-bspm \
        && echo "suppressMessages(bspm::enable())" >> /etc/R/Rprofile.site \
        && echo "options(pkgType=\"binary-source\")" >> /etc/R/Rprofile.site \
        && echo 'APT::Install-Recommends "false";' > /etc/apt/apt.conf.d/90local-no-recommends \
        && chgrp 1000 /usr/local/lib/R/site-library \
        && install.r remotes

CMD ["bash"]
