FROM debian:12
RUN apt-get update && apt-get install -y openssh-server python3 sudo iproute2 && \
    mkdir /var/run/sshd && \
    useradd -m -s /bin/bash ansible_user && \
    echo "ansible_user:ansible123" | chpasswd && \
    usermod -aG sudo ansible_user && \
    echo "ansible_user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
