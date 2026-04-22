FROM debian:bookworm-slim

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        openssh-server \
        passwd \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -m -s /bin/bash user \
    && echo 'user:password' | chpasswd \
    && mkdir -p /run/sshd \
    && ssh-keygen -A \
    && sed -i 's@session\\s\\+required\\s\\+pam_loginuid.so@session optional pam_loginuid.so@' /etc/pam.d/sshd

COPY sshd_config /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D", "-e"]
