FROM ubuntu:focal AS base
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y software-properties-common curl git build-essential sudo && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*

FROM base AS home
ARG user=abf
ARG COMPONENTS=neovim
ENV HOME_HEADLESS=1
ENV HOME_ALLOW_ROOT=0

RUN addgroup --gid 1000 "$user" && \
    adduser --gecos "$user" --uid 1000 --gid 1000 --disabled-password "$user" && \
    adduser "$user" sudo && \
    echo "$user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

COPY --chown=${user}:${user} . /home/${user}/home
USER ${user}
WORKDIR /home/${user}/home
RUN ./ansible/install linux ${COMPONENTS}

CMD ["tail", "-f", "/dev/null"]
