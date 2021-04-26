FROM ubuntu:latest
LABEL maintainer="Ankur Dhakar"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update &&     apt-get -qy full-upgrade &&     apt-get install -qy git &&     apt-get install -qy openssh-server &&     sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&     mkdir -p /var/run/sshd &&     apt-get install -qy openjdk-8-jdk &&     apt-get install -qy maven &&     apt-get -qy autoremove &&     adduser --quiet jenkins &&     echo "jenkins:jenkins" | chpasswd &&     mkdir /home/jenkins/.m2

COPY authorized_keys  /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.m2/ &&     chown -R jenkins:jenkins /home/jenkins/.ssh/
EXPOSE 22
COPY config /home/jenkins/.kube/config
COPY kubectl /usr/local/bin/
COPY ca.crt /home/jenkins/ca.crt
COPY client.crt /home/jenkins/client.crt
COPY client.key /home/jenkins/client.key
RUN apt-get -qy install curl
CMD ["/usr/sbin/sshd","-D"]
