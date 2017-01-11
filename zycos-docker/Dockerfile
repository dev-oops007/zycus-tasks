#######Python 2.7, TOMcat7 and MONGOdb2.6 on Base Centos 6.7#######3

From centos:centos6.7
# File Author / Maintainer
MAINTAINER      DevVrat Tomar <tomardev007@gmail.com>


#####Dependencies for Python ,Tomcat and  MOngo  ####3#
RUN yum  update -y && \
    yum groupinstall -y development

RUN yum install -y gcc \
    wget \
    tar \
    zlib-dev \
    openssl-devel \
    sqlite-devel \
    bzip2-devel \
    java-1.7.0-openjdk-devel

#######3Pyhton 2.7########
RUN cd /tmp && \
    wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tgz && \
    tar xzf Python-2.7.12.tgz && \
    cd Python-2.7.12 && \
    ./configure && \
    make altinstall

##TomCat 7 Installation using tar file ##
RUN cd /usr/local && \
    mkdir tomcat7 && \
    wget  http://www.gtlib.gatech.edu/pub/apache/tomcat/tomcat-7/v7.0.73/bin/apache-tomcat-7.0.73.tar.gz && \ 
    tar  -xvzf apache-tomcat-7.0.73.tar.gz && \
    mv apache-tomcat-7.0.73/* tomcat7 && \
    cd tomcat7/bin && \
    ./startup.sh 

##adding users and password in xml file for Apache tomcat login page  
ADD tomcat-users.xml /usr/local/tomcat7/conf

###staring tomcat service at boot time of docker 
CMD ./usr/local/tomcat7/bin/startup.sh


##adding mongo repo
#ADD mongodb.repo /etc/yum.repos.d/
RUN echo -e '[mongodb]\nname=MongoDB Repository\nbaseurl=http://downloads-distro.mongodb.org/repo/redhat/os/x86_64/\ngpgcheck=0\nenabled=1'>/etc/yum.repos.d/mongodb.repo
 
#ADD mongodb.conf /etc/

##installing mongo db  server 
RUN yum update -y
RUN yum install -y  mongodb-org


###redefining permissions on 
RUN chown -R mongod:mongod /var/lib/mongo

##setting mongoi user
USER mongod

#mount system  directory for mongo 
VOLUME /var/lib/mongo

## Set environment variable
ENV HOME /var/lib/mongo

# Working directory
WORKDIR /var/lib/mongo


##tomcat and mongo port exposing

EXPOSE  8080 27017
##when container run then mongod start by default
ENTRYPOINT /bin/mongod

CMD ["-f", "/etc/mongod.conf"] 

