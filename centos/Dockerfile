FROM centos

RUN yum install -y openssh-server && \
    yum install -y python3 &&\
    useradd -d /home/jenkins -u 1000 jenkins && \
    echo "jenkins:1234" | chpasswd &&\
    /usr/bin/ssh-keygen -A &&\
    rm -rf /run/nologin
EXPOSE 22

 
RUN mkdir /home/jenkins/.ssh && \
    chmod 700 /home/jenkins/.ssh &&\
    touch /home/jenkins/.ssh/authorized_keys 
    

COPY id_rsa.pub /home/jenkins/.ssh/authorized_keys

RUN chown -R jenkins:jenkins /home/jenkins &&\
    chmod 700 /home/jenkins/.ssh/authorized_keys &&\
    yum -y install mysql &&\
    curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh > /home/jenkins/install.sh &&\
    chown jenkins:jenkins /home/jenkins/install.sh &&\
    chmod +x /home/jenkins/install.sh &&\
    su jenkins -c "/home/jenkins/install.sh  --accept-all-defaults" &&\
    mkdir /home/jenkins/.oci

COPY ["config", "oci_cli_rc", "amit-mum-api-key.pem", "/home/jenkins/.oci/"]
RUN chown jenkins:jenkins -R /home/jenkins/.oci

CMD /usr/sbin/sshd -D
