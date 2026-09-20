FROM rockylinux:9.3.20231119

RUN dnf install -y epel-release dnf-plugins-core && \
    dnf config-manager --set-enabled crb && \
    dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo && \
    dnf install -y \
        openssh-server \
        fastfetch \
        docker-ce-cli \
        docker-compose-plugin && \
    dnf clean all

RUN ssh-keygen -A && \
    echo 'root:rockylinux' | chpasswd && \
    sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN echo "fastfetch" >> /root/.bashrc

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]