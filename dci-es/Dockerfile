FROM centos:7

LABEL name="DCI ES" version="0.0.1"
MAINTAINER DCI Team <distributed-ci@redhat.com>

ENV ES_HOME /home/elasticsearch

RUN rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch
RUN echo -e "[elasticsearch-2.x]\n\
name=Elasticsearch repository for 2.x packages\n\
baseurl=http://packages.elastic.co/elasticsearch/2.x/centos\n\
gpgcheck=1\n\
gpgkey=http://packages.elastic.co/GPG-KEY-elasticsearch\n\
enabled=1" > /etc/yum.repos.d/elasticsearch.repo
RUN yum install -y elasticsearch java-1.8.0-openjdk hostname && \
    yum clean all

RUN mkdir -p ${ES_HOME}/config ${ES_HOME}/logs ${ES_HOME}/data

RUN cp -r /usr/share/elasticsearch/* ${ES_HOME}

RUN chown -R elasticsearch:elasticsearch ${ES_HOME}

USER elasticsearch

RUN echo "network.host: 0.0.0.0" > ${ES_HOME}/config/elasticsearch.yml

EXPOSE 9200 9300

CMD ["sh", "-c", "${ES_HOME}/bin/elasticsearch"]
