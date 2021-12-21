## Rocker r-bspm

The `r-bspm` Dockerfiles from the [Rocker Project](https://www.rocker-project.org/)
provide basic building blocks using Ubuntu and Debian with the
[bspm](https://cran.r-project.org/package=bspm) package to bridge from the R package
management to the system package manager.

Note that there is _no 'latest' tag_ as we offer Ubuntu, Debian, Fedora, and
OpenSUSE builds so 'latest' cannot properly map.  See the [Docker Hub
page](https://hub.docker.com/r/rocker/r-bspm/tags) for available tags. For
for example to get Debian testing use

    docker pull rocker/r-bspm:testing

Documentation is being added at the [Wiki](https://github.com/rocker-org/rocker/wiki). Please file
issue tickets at [the rocker/ issue tracker](https://github.com/rocker-org/rocker/issues). 
