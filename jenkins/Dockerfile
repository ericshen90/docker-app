FROM ubuntu:18.04

MAINTAINER EricShen <ahsbt@126.com>

ENV JAVA_MAJOR_VERSION=8
ENV JAVA_BUILD_NUMBER=152
ENV TOMCAT_VERSION=8.5.47
ENV TZ=Asia/Shanghai

# 修改软件源
RUN echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse' > /etc/apt/sources.list && \
    echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse' >> /etc/apt/sources.list && \
    echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse' >> /etc/apt/sources.list && \
    echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse' >> /etc/apt/sources.list && \
    apt-get update -y && \
    apt-get clean

# 修改时区
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 安装 Tomcat
RUN mkdir -p /usr/local/tomcat
WORKDIR /usr/local/tomcat
COPY apache-tomcat-${TOMCAT_VERSION}.tar.gz /usr/local/tomcat
RUN tar -zxvf apache-tomcat-${TOMCAT_VERSION}.tar.gz
#&& \
#    rm -fr apache-tomcat-${TOMCAT_VERSION}

# 安装 Java
RUN mkdir -p /usr/local/java
WORKDIR /usr/local/java
COPY jdk-${JAVA_MAJOR_VERSION}u${JAVA_BUILD_NUMBER}-linux-x64.tar.gz /usr/local/java
RUN tar -zxvf jdk-${JAVA_MAJOR_VERSION}u${JAVA_BUILD_NUMBER}.tar.gz
#&& \
#    rm -fr jdk-${JAVA_MAJOR_VERSION}u${JAVA_BUILD_NUMBER}.tar.gz

# 配置环境变量
ENV JAVA_HOME /usr/local/java/jdk1.${JAVA_MAJOR_VERSION}.0_${JAVA_BUILD_NUMBER}
ENV PATH $PATH:$JAVA_HOME/bin

WORKDIR /
