FROM cirit/oracle-java:latest

MAINTAINER Cagdas Cirit <cagdascirit@gmail.com>

ENV TOMCAT_MAJOR=8
ENV TOMCAT_VERSION=8.0.26
ENV CATALINA_HOME=/usr/local/apache-tomcat-${TOMCAT_VERSION}
ENV PATH=${CATALINA_HOME}/bin:${PATH}

RUN apt-get -y update && \
	apt-get -y install wget 

RUN wget https://www.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
	tar -xzf apache-tomcat-${TOMCAT_VERSION}.tar.gz -C /usr/local/ 

RUN rm -rf apache-tomcat-${TOMCAT_VERSION}.tar.gz \
			${CATALINA_HOME}/bin/*.bat && \
	apt-get -y remove wget && \
	apt-get -y --purge autoremove && \
	apt-get -y clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 8080

ENTRYPOINT ["catalina.sh","run"]
