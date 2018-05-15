FROM       centos:7.3.1611
LABEL      maintainer="prash.balan@theweflex.com" \
           version="6.2.4" \
           project="elasticsearch"
ARG        APP_HOME=/opt/deployment
RUN        useradd weflex -d ${APP_HOME} -u 1000 && \
           yum install wget -y -q

# add java support for elasticsearch
ARG        JAVA_VERSION=8u172
ARG        JRE_DIR=jre1.8.0_172
ARG        JAVA_BUILD=b11

RUN        wget -q -O /tmp/jdk-linux-x64.tar.gz --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
           "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}-${JAVA_BUILD}/a58eab1ec242421181065cdc37240b08/jre-${JAVA_VERSION}-linux-x64.tar.gz"  && \
           tar -xzf /tmp/jdk-linux-x64.tar.gz -C /usr/local && \
           rm -f /usr/local/${JRE_DIR}/{COPYRIGHT LICENSE README THIRDPARTYLICENSEREADME.txt Welcome.html} && \
           ln -sf /usr/local/${JRE_DIR}/bin/java /usr/local/bin && \
           ln -sf /usr/local/${JRE_DIR} /usr/local/jre && \
           rm -rf /tmp/jdk-linux-x64.tar.gz
ENV        JAVA_HOME=/usr/local/${JRE_DIR}
ENV        LANG en_US.UTF-8
ENV        PATH=$JAVA_HOME/bin:$PATH

# add elasticsearch
ARG        ELASTIC_VERSION=6.2.4
ARG        ES_HOME=/usr/local/elasticsearch
RUN        useradd -u 403 elasticsearch &&\
           wget -q -O /tmp/elasticsearch.tar.gz https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${ELASTIC_VERSION}.tar.gz && \
           tar -xzf /tmp/elasticsearch.tar.gz -C /usr/local && \
           chown -R elasticsearch:elasticsearch /usr/local/elasticsearch-${ELASTIC_VERSION} && \
           sed -e '/-Xmx2g/d' -e  '/-Xms2g/d' -i /usr/local/elasticsearch-${ELASTIC_VERSION}/config/jvm.options && \
           ln -sf /usr/local/elasticsearch-${ELASTIC_VERSION} ${ES_HOME} && \
           rm -rf /tmp/elasticsearch.tar.gz
USER       elasticsearch
ENV        JAVA_HOME=/usr/local/jre \
	         ES_HOME=${ES_HOME}

EXPOSE     9200 9300
ENTRYPOINT ["/usr/local/elasticsearch/bin/elasticsearch"]
