FROM debian:buster

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get --assume-yes --quiet update && \
    apt-get --assume-yes --quiet install ansible git

#Debug packages
RUN DEBIAN_FRONTEND=noninteractive apt-get --assume-yes --quiet install vim

RUN adduser --disabled-password --gecos "" user
USER user
WORKDIR /home/user/

# The FORCE_REBUILD variable is not used by git but forces docker to rebuild
# from this layer, essentially forcing a git clone
ARG FORCE_REBUILD=dummy
RUN FORCE_REBUILD=${FORCE_REBUILD} git clone https://github.com/NiCalderon/dotfiles-bootstrap.git

WORKDIR /home/test/dotfiles-bootstrap/
RUN ansible-galaxy install -r requirements.yml
RUN ansible-playbook playbook.yml

WORKDIR /home/test/

ENTRYPOINT ["sh"]
