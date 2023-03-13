FROM jenkins/jenkins

USER root

 
RUN apt-get update && apt-get -y install python3 &&\
    apt-get -y install python3-pip &&\
    pip install ansible --upgrade 

USER jenkins
#RUN mkdir $HOME/ansible 
COPY ["hosts", "id_rsa", "$HOME/ansible/"]
