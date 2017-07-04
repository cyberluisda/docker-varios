FROM cyberluisda/flume:1.7.0-1.1.0

MAINTAINER Luis David Barrios Alfonso (luis.david.barrios@ericsson.com)

# ADD iVi agents configurations
# /var/log/flume is created by defalt by cyberluisda/flume image but
# We add here to remember that we must create if we save logs to different path
RUN mkdir -p /etc/flume /var/log/flume
COPY files/agents/* /etc/flume/

CMD [ "dummy" ]
