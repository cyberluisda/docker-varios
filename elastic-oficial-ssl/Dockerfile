FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.2
MAINTAINER Luis David Barrios (luis.david.barrios@outlook.com)

# SSl configurationADD files/certificates /usr/share/config/
ADD files/certificates /usr/share/elasticsearch/config/certificates/
RUN  echo 'xpack.ssl.key: /usr/share/elasticsearch/config/certificates/node.key' >> /usr/share/elasticsearch/config/elasticsearch.yml \
  && echo 'xpack.ssl.certificate: /usr/share/elasticsearch/config/certificates/node.crt' >> /usr/share/elasticsearch/config/elasticsearch.yml \
  && echo 'xpack.ssl.certificate_authorities: [ "/usr/share/elasticsearch/config/certificates/ca.crt" ]' >> /usr/share/elasticsearch/config/elasticsearch.yml \
  && echo 'xpack.security.http.ssl.enabled: true' >> /usr/share/elasticsearch/config/elasticsearch.yml \
  && echo 'xpack.security.transport.ssl.enabled: true' >> /usr/share/elasticsearch/config/elasticsearch.yml

# Prepare for only one node
ENV discovery.type single-node
