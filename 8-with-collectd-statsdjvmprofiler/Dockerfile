FROM cirit/oracle-java:server-jre-8u60-with-collectd

MAINTAINER Cagdas Cirit <cagdascirit@gmail.com>

ENV TOMCAT_MAJOR=8
ENV TOMCAT_VERSION=8.0.27
ENV CATALINA_HOME=/usr/local/tomcat
ENV PATH=${CATALINA_HOME}/bin:${PATH}

RUN mkdir -p "$CATALINA_HOME" && \
	echo "deb http://httpredir.debian.org/debian stretch main contrib" | tee -a /etc/apt/sources.list && \
	apt-get -y update && \
	apt-get -y install \
	curl \
	supervisor 

RUN curl -fSL https://www.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz -o tomcat.tar.gz && \
	tar -xzf tomcat.tar.gz --strip-components=1 -C ${CATALINA_HOME}

RUN rm -rf tomcat.tar.gz \
			${CATALINA_HOME}/bin/*.bat && \
	apt-get -y remove curl && \
	apt-get -y --purge autoremove && \
	apt-get -y clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD supervisord.conf /etc/supervisor/conf.d/
ADD statsd-jvm-profiler-0.8.3-SNAPSHOT.jar /var/lib/

EXPOSE 8080

ENTRYPOINT ["supervisord"]
