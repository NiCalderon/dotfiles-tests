FROM debian:buster

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get --assume-yes --quiet update && \
    apt-get --assume-yes --quiet install sudo ansible git

#Debug packages
RUN DEBIAN_FRONTEND=noninteractive apt-get --assume-yes --quiet install vim

ARG ansible_user=ansible
RUN adduser --disabled-password --gecos "" $ansible_user && \
    echo $ansible_user:$ansible_user | chpasswd && \
    usermod -aG sudo $ansible_user
USER $ansible_user
WORKDIR /home/$ansible_user/

# The FORCE_REBUILD variable is not used by git but forces docker to rebuild
# from this layer, essentially forcing a git clone
ARG FORCE_REBUILD=dummy
RUN FORCE_REBUILD=${FORCE_REBUILD} git clone https://github.com/NiCalderon/dotfiles-bootstrap.git

WORKDIR /home/$ansible_user/dotfiles-bootstrap/
RUN ansible-galaxy install -r requirements.yml
RUN ansible-playbook playbook.yml --extra-vars "ansible_become_pass=$ansible_user"

WORKDIR /home/$ansible_user/

ENTRYPOINT ["bash", "--login"]
