FROM rockylinux:9.3.20231119

RUN dnf install -y epel-release && \
    dnf install -y openssh-server fastfetch && \
    dnf clean all

RUN ssh-keygen -A && \
    echo 'root:rockylinux' | chpasswd && \
    sed -i 's/.*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN echo "fastfetch" >> /root/.bashrc

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]