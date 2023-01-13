FROM opensuse/tumbleweed:latest

LABEL org.label-schema.license="GPL-2.0" \
      org.label-schema.vcs-url="https://github.com/rocker-org/rocker" \
      maintainer="Iñaki Ucar <iucar@fedoraproject.org>"

ENV URL  https://download.opensuse.org/repositories/devel:/languages:/R:
ENV CRAN autoCRAN
ENV OS   openSUSE_Tumbleweed
ENV KEY  repodata/repomd.xml.key

RUN zypper -n install curl \
    && zypper -n ar -r ${URL}/${CRAN}/${OS}/devel:languages:R:${CRAN}.repo \
    && curl ${URL}/${CRAN}/${OS}/${KEY} > /tmp/${CRAN}.key \
    && rpm --import /tmp/${CRAN}.key \
    && rm -rf /tmp/*

RUN zypper -n install \
        R gcc-c++ gcc-fortran pkgconfig libbz2-devel libX11-devel zlib-devel \
        tcl-devel tk-devel tre-devel pcre2-devel xz-devel libicu-devel \
        python3-dnf \
    && ln -s /etc/zypp/repos.d /etc/yum.repos.d

RUN echo "options(repos='https://cloud.r-project.org')" > \
        /usr/lib64/R/etc/Rprofile.site \
    && Rscript -e 'install.packages(c("bspm", "littler"))' \
    && echo "bspm::enable()" >> /usr/lib64/R/etc/Rprofile.site \
    && mkdir -p /usr/local/lib/R/site-library

RUN ln -s /usr/lib64/R/library/littler/bin/r /usr/local/bin/r \
    && ln -s /usr/lib64/R/library/littler/examples/install.r \
        /usr/local/bin/install.r \
    && ln -s /usr/lib64/R/library/littler/examples/install2.r \
        /usr/local/bin/install2.r \
    && ln -s /usr/lib64/R/library/littler/examples/installGithub.r \
        /usr/local/bin/installGithub.r \
    && ln -s /usr/lib64/R/library/littler/examples/testInstalled.r \
        /usr/local/bin/testInstalled.r \
    && install.r remotes

CMD ["bash"]
