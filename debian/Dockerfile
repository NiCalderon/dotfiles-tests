FROM debian:buster

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get --assume-yes --quiet update && \
    apt-get --assume-yes --quiet install ansible git

#Debug packages
RUN DEBIAN_FRONTEND=noninteractive apt-get --assume-yes --quiet install vim

RUN adduser --disabled-password --gecos "" test
USER test
WORKDIR /home/test/

ARG FORCE_REBUILD=dummy
RUN FORCE_REBUILD=${FORCE_REBUILD} git clone https://github.com/NiCalderon/dotfiles-bootstrap.git

ENTRYPOINT ["sh"]