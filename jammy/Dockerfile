## Emacs, make this -*- mode: sh; -*-

FROM rocker/r-ubuntu:22.04

LABEL org.label-schema.license="GPL-2.0" \
      org.label-schema.vcs-url="https://github.com/rocker-org/rocker" \
      maintainer="Dirk Eddelbuettel <edd@debian.org>"

## This was not needed before but we need it now
#ENV DEBIAN_FRONTEND noninteractive

RUN rm -f /etc/apt/sources.list.d/c2d4u*list \
        && apt update -qq \
        && install.r bspm remotes \
        && echo "suppressMessages(bspm::enable())" >> /etc/R/Rprofile.site \
        && echo "options(bspm.version.check=FALSE)" >> /etc/R/Rprofile.site \
        && echo 'APT::Install-Recommends "false";' > /etc/apt/apt.conf.d/90local-no-recommends \
        && chgrp -R 1000 /usr/local/lib/R/site-library

CMD ["bash"]
