FROM centos:centos6
MAINTAINER  Ankit Mittal <ankit@gmail.com.com>

RUN yum -y update; yum clean all

RUN yum -y install httpd php

RUN echo "Bifrost Website is hosted inside a container" > /var/www/html/index.html

EXPOSE 80

ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
