FROM jenkins/jenkins:2.138.4
USER root

#Pre-Install Jenkins Plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

#Installing Docker
#RUN apt-get update && apt-get install vim software-properties-common apt-transport-https ca-certificates -y; \
#curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -;\
#add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/debian  $(lsb_release -cs) stable";\
#apt-get update && apt-get install docker-ce -y
# by me
RUN apt-get update && apt-get install vim software-properties-common apt-transport-https ca-certificates -y
RUN mkdir /usr/tmp
COPY *.deb /usr/tmp/
RUN apt-get install iptables -y
RUN dpkg -i /usr/tmp/*.deb

#Installing kubectl from Docker
#RUN curl -fsSL http://mirrors.ustc.edu.cn/kubernetes/apt/dists/kubernetes-xenial/Release.gpg | apt-key add -;\
#touch /etc/apt/sources.list.d/kubernetes.list;\
#echo "deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list;\
#apt-get update && apt-get install -y kubectl --allow-unauthenticated
# by me
COPY kubectl /usr/bin/    
RUN chmod +x /usr/bin/kubectl

RUN rm -rf /usr/tmp

# Grant jenkins user group access to /var/run/docker.sock
#RUN addgroup --gid 1001 dsock
RUN gpasswd -a jenkins docker 
RUN gpasswd -a jenkins root
USER jenkins
