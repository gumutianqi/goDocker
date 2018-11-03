# CentOS7 based base image with Oracle JDK 8u192

FROM centos:7

RUN curl -LO --insecure --junk-session-cookies --location --remote-name --silent \
--header "Cookie: oraclelicense=accept-securebackup-cookie" \
http://download.oracle.com/otn-pub/java/jdk/8u192-b12/750e1c8617c5452694857ad95c3ee230/jdk-8u192-linux-x64.rpm && \
yum localinstall -y jdk-8u192-linux-x64.rpm && \
yum clean all && \
rm jdk-8u192-linux-x64.rpm && \
curl -L https://alibaba.github.io/arthas/install.sh | sh

ENV JAVA_HOME /usr/java/default

ENV JRE_HOME=$JAVA_HOME/jre \
    CLASSPATH=$JAVA_HOME/lib:$JAVA_HOME/jre/lib \
    PATH=$JAVA_HOME/bin:$PATH
