# TODO: evalute 5.5.2-alpine here!
# Official images: https://www.docker.elastic.co/
FROM docker.elastic.co/elasticsearch/elasticsearch:5.5.0

RUN \
  mv /usr/share/elasticsearch/plugins/x-pack /usr/share/elasticsearch/plugins/.removing-x-pack && \
  mv /usr/share/elasticsearch/plugins/.removing-x-pack /usr/share/elasticsearch/plugins/x-pack && \
  /usr/share/elasticsearch/bin/elasticsearch-plugin remove x-pack
