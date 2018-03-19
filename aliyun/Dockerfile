FROM centos:7
MAINTAINER nopost<nopost@vip.qq.com>
LABEL version="5.7"
RUN yum -y update \
 && yum -y install wget net-tool openssh-server; yum clean all
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN sed -ri 's/session    required     pam_loginuid.so/#session    required     pam_loginuid.so/g' /etc/pam.d/sshd
RUN mkdir -p /root/.ssh && chown root.root /root && chmod 700 /root/.ssh
RUN echo 'root:nopost.cn' | chpasswd
RUN wget -O install.sh http://download.bt.cn/install/install.sh \
 && printf "y\n0"|bash ./install.sh
RUN echo -e "#! /bin/bash\n  cd /www/server/panel \n  python tools.pyc panel nopost.cn \n /etc/init.d/bt start\n /usr/sbin/sshd -D" > /hello.sh
RUN chmod +x /hello.sh
EXPOSE 21 22 80 443 888 3306 8888
VOLUME ["/www/wwwroot"] 
VOLUME ["/www/backup"]
CMD /hello.sh
