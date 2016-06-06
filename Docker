FROM ubuntu:14.04
MAINTAINER Jimmy Mokwena <sir.jimmy@ymail.com>

ENV WSO2MDM_VERSION 2.0.1

RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections

RUN apt-get update
RUN apt-get -y upgrade

# Requirements
RUN apt-get install -y git software-properties-common tar unzip wget nano

# Java
RUN apt-get -y install python-software-properties
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN apt-get install -y --no-install-recommends oracle-java8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# WSO2 EMM
RUN wget --user-agent=testuser --referer=http://connect.wso2.com/wso2/getform/reg/new_product_download http://product-dist.wso2.com/products/enterprise-mobility-manager/$WSO2MDM_VERSION/wso2emm-$WSO2MDM_VERSION.zip
RUN unzip wso2emm-$WSO2MDM_VERSION.zip
ENV WSO2MDM_HOME /wso2emm-$WSO2MDM_VERSION
ENV PATH $PATH:$WSO2MDM_HOME/bin

# Expose
EXPOSE 9763 9443

# Start
CMD ["/bin/bash", "-c", "wso2server.sh", "start"]	

# Clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*