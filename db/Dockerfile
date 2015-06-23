# Requirements:
#   - download latest MarkLogic 8 (MarkLogic-8.0-....x86_64.rpm) from http://developer.marklogic.com/download 
#     into the same directory like this Dockerfile
#
# Build your own image:
#     docker build -t centos-marklogic8 .
#
# Start a new container with this image:
#     docker run -p 8000:8000 -p 8001:8001 -p 8002:8002 -p 9060:9060 -p 9061:9061 -p 9062:9062 -p 9063:9063 -p 9064:9064 --name="wm14-demo" centos-marklogic8
#
# If you are interested to connect into the container:
#     docker exec -i -t wm14-demo bash

FROM ml8-prereqs
MAINTAINER Patrick McElwee <patrick.mcelwee@marklogic.com>

RUN yum -y install vim

# Install MarkLogic
WORKDIR /tmp
ADD MarkLogic-8.0-20150623.x86_64.rpm /tmp/MarkLogic.rpm

RUN yum -y install /tmp/MarkLogic.rpm

# Expose MarkLogic Server ports
EXPOSE 7997 7999 8000 8001 8002 8111 9060 9061 9062 9063 9064

# Define default command (which avoids immediate shutdown)
CMD /opt/MarkLogic/bin/MarkLogic && tail -f /data/Logs/ErrorLog.txt

