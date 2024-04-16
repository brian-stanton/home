# FROM ubuntu:jammy AS base
FROM ubuntu:focal AS base
WORKDIR /usr/local/bin
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y software-properties-common curl git build-essential sudo && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible && \
    apt-get clean autoclean && \
    apt-get autoremove --yes

FROM base AS home
ARG TAGS
RUN addgroup --gid 1000 abf
RUN adduser --gecos abf --uid 1000 --gid 1000 --disabled-password abf
RUN adduser abf sudo
RUN echo 'abf ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
USER abf
WORKDIR /home/abf

# Don't need to run this here because we're just gonna copy, but in a new system, we'll need to grab the files
# RUN git clone https://github.com/brian-stanton/home /code
COPY . .
RUN ansible-playbook $TAGS ssh2.yml

FROM home
CMD [ "tail",  "-f", "/dev/null" ]

