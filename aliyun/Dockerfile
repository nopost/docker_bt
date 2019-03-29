FROM centos:latest
MAINTAINER nopost<nopost@vip.qq.com>
LABEL version="6.9"
RUN yum -y update \
&& yum -y install wget net-tool openssh-server initscripts; yum clean all \
&& ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key \
&& ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key \
&& ssh-keygen -q -N "" -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key \
&& ssh-keygen -q -N "" -t ed25519 -f /etc/ssh/ssh_host_ed25519_key \
&& sed -ri 's/session    required     pam_loginuid.so/#session    required     pam_loginuid.so/g' /etc/pam.d/sshd \
&& mkdir -p /root/.ssh && chown root.root /root && chmod 700 /root/.ssh \
&& echo 'root:nopost.cn' | chpasswd \
&& wget -O install.sh http://download.bt.cn/install/install_6.0.sh \
&& printf "y\n0"|bash ./install.sh \
&& echo -e "#!/bin/bash\n python /www/server/panel/tools.pyc panel nopost.cn \n service bt start \n/usr/sbin/sshd -D\n" > /hello.sh \
&& chmod +x /hello.sh \
EXPOSE 21 22 80 443 888 3306 8888 
VOLUME ["/sys/fs/cgroup"] 
VOLUME ["/www/wwwroot"] 
VOLUME ["/www/backup"]
CMD /usr/sbin/init && /hello.sh
