FROM ghostsquad/docker-java8

RUN cd /opt &&\
    wget --progress=dot:mega https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-tgz -O atlassian-plugin-sdk.tar.gz &&\
    mkdir atlassian-plugin-sdk &&\
    tar -xvzf atlassian-plugin-sdk.tar.gz --strip-components 1 -C atlassian-plugin-sdk &&\
    rm atlassian-plugin-sdk.tar.gz &&\
    ln -s /opt/atlassian-plugin-sdk/bin /usr/local/bin/atlassian-plugin-sdk &&\
    yum install -y epel-release &&\
    yum install -y python-setuptools python-pip &&\
    pip install supervisor &&\
    mkdir -p /etc/supervisord &&\
    mkdir -p /var/log/supervisor &&\
    mkdir -p /home/atlassian/amps-standalone/target &&\
    yum clean all

VOLUME /opt/atlassian-plugin-sdk

ENV PATH $PATH:/opt/atlassian-plugin-sdk/bin

WORKDIR /opt/atlassian-plugin-sdk

# RUN atlas-version
RUN atlas-run-standalone --product jira --bundled-plugins com.atlassian.jwt:jwt-plugin:1.1.0,com.atlassian.bundles:json-schema-validator-atlassian-bundle:1.0.4,com.atlassian.webhooks:atlassian-webhooks-plugin:1.0.6,com.atlassian.upm:atlassian-universal-plugin-manager-plugin:2.17.14-D20140902T224549,com.atlassian.plugins:atlassian-connect-plugin:1.1.4 --jvmargs -Datlassian.upm.on.demand=true

EXPOSE 2990