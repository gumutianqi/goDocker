# CentOS based base image with Oracle JDK 8
# Inspired by lwieske/java-8, but with fewer layers

FROM centos:7

RUN curl -LO --insecure --junk-session-cookies --location --remote-name --silent \
--header "Cookie: oraclelicense=accept-securebackup-cookie" \
http://download.oracle.com/otn-pub/java/jdk/8u192-b12/750e1c8617c5452694857ad95c3ee230/jdk-8u192-linux-x64.rpm && \
yum localinstall -y jdk-8u192-linux-x64.rpm && \
yum clean all && \
rm jdk-8u74-linux-x64.rpm \
curl -L https://alibaba.github.io/arthas/install.sh | sh

ENV JAVA_HOME /usr/java/default
