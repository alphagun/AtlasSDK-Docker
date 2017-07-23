FROM ghostsquad/docker-java8

RUN cd /opt &&\
    wget --progress=dot:mega https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-tgz -O atlassian-plugin-sdk.tar.gz &&\
    mkdir atlassian-plugin-sdk

VOLUME /opt/atlassian-plugin-sdk

RUN tar -xvzf atlassian-plugin-sdk.tar.gz --strip-components 1 -C atlassian-plugin-sdk &&\
    rm atlassian-plugin-sdk.tar.gz &&\
    ln -s /opt/atlassian-plugin-sdk/bin /usr/local/bin/atlassian-plugin-sdk &&\
    yum install -y epel-release &&\
    yum install -y python-setuptools python-pip &&\
    pip install supervisor &&\
    mkdir -p /etc/supervisord &&\
    mkdir -p /var/log/supervisor &&\
    mkdir -p /home/atlassian/amps-standalone/target &&\
    yum clean all

ENV PATH $PATH:/opt/atlassian-plugin-sdk/bin

WORKDIR /opt/atlassian-plugin-sdk

RUN atlas-version