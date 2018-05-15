FROM       centos:7.3.1611
LABEL      maintainer="prash.balan@theweflex.com" \
           version="6.2.4" \
           project="kibana"
# add kibana
ARG        KIBANA_VERSION=6.2.4
ENV        container docker \
           PACKAGE_VERSION=${KIBANA_VERSION}
ARG        APP_HOME=/usr/local/kibana
RUN        yum install -y -q wget && \
           groupadd -g 405 kibana && \
           useradd -u 405 -g 405 kibana && \
           wget -q -O /tmp/kibana.tar.gz https://artifacts.elastic.co/downloads/kibana/kibana-${KIBANA_VERSION}-linux-x86_64.tar.gz && \
           tar -xzf /tmp/kibana.tar.gz -C /usr/local && \
           ln -sf /usr/local/kibana-${KIBANA_VERSION}-linux-x86_64 ${APP_HOME} && \
           mkdir -p /var/log/kibana /etc/kibana && \
           rm -rf /tmp/kibana.tar.gz && \
           touch /var/log/kibana/kibana.log
COPY       setup/config/kibana.yml /etc/kibana/kibana.yml
ADD        setup/scripts /usr/local/kibana/
RUN        chown -R kibana:kibana /usr/local/kibana-${KIBANA_VERSION}-linux-x86_64 /var/log/kibana /etc/kibana && \
	         /usr/local/kibana/bin/kibana-plugin install https://github.com/sivasamyk/logtrail/releases/download/v0.1.27/logtrail-${KIBANA_VERSION}-0.1.27.zip
COPY       setup/config/logtrail.json /usr/local/kibana/plugins/logtrail/logtrail.json
EXPOSE     5601
ENTRYPOINT ["/usr/local/kibana/kibana.sh"]
