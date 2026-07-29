FROM rockylinux:9
RUN dnf install -y openssh-server python3 sudo passwd procps-ng && \
    ssh-keygen -A && \
    useradd -m -s /bin/bash ansible_user && \
    echo "ansible_user:ansible123" | chpasswd && \
    usermod -aG wheel ansible_user && \
    echo "ansible_user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
