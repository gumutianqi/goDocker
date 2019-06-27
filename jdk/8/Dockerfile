# CentOS7 based base image with Oracle JDK 8u192
FROM centos:7

LABEL author="larrykoo@126.com" \
      Description="基于CentOS7,安装了oracle jdk8u192"  Version="1.0"

RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup && \
    curl -o /etc/yum.repos.d/CentOS-Base.repo --progress-bar http://mirrors.163.com/.help/CentOS7-Base-163.repo && \
    yum clean all && yum makecache && \
    yum -y install telnet sysstat unzip && \
    yum clean all

## install jdk8
COPY jdk-8u192-linux-x64.rpm jdk-8u192-linux-x64.rpm
RUN yum localinstall -y jdk-8u192-linux-x64.rpm && \
    yum clean all && \
    rm jdk-8u192-linux-x64.rpm

## 安装 alibaba anrhas 工具: https://github.com/alibaba/arthas
RUN curl -O https://alibaba.github.io/arthas/arthas-boot.jar

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

## create a JAVA_HOME
ENV JAVA_VERSION 8u192
ENV JAVA_HOME /usr/java/default
ENV JRE_HOME=$JAVA_HOME/jre \
    CLASSPATH=$JAVA_HOME/lib:$JAVA_HOME/jre/lib \
    PATH=$JAVA_HOME/bin:$PATH:${CLASSPATH}
