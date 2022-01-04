FROM archlinux:latest

LABEL org.label-schema.license="GPL-2.0" \
      org.label-schema.vcs-url="https://github.com/rocker-org/bspm" \
      maintainer="Iñaki Ucar <iucar@fedoraproject.org>"

RUN echo -e "\n[desolve]\nServer = https://desolve.ru/archrepo/\$arch" \
    >> /etc/pacman.conf \
    && pacman -Syu --noconfirm \
        sudo shadow make gcc-fortran \
        r pyalpm python-{dbus,gobject}

RUN echo "options(repos='https://cloud.r-project.org')" \
        > /usr/lib64/R/etc/Rprofile.site \
    && Rscript -e 'install.packages(c("bspm", "littler"))' \
    && echo "bspm::enable()" >> /usr/lib64/R/etc/Rprofile.site \
    && echo "options(bspm.sudo=TRUE)" >> /usr/lib64/R/etc/Rprofile.site

RUN useradd -m docker \
    && echo "docker ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/docker-user \
    && chmod 0440 /etc/sudoers.d/docker-user \
    && echo 'R_LIBS_SITE=/usr/local/lib/R/site-library:/usr/lib64/R/library' \
        >> /usr/lib64/R/etc/Renviron \
    && mkdir -p /usr/local/lib/R/site-library \
    && chown 1000:1000 /usr/local/lib/R/site-library

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
