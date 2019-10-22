FROM centos:7
MAINTAINER The CentOS Project <cloud-ops@centos.org>
LABEL Vendor="CentOS" \
      License=GPLv2 \
      Version=2.4.6-40


RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install httpd mod_ssl php && \
    yum clean all 
    
WORKDIR /var/www/html/site
WORKDIR /etc/httpd/tls
    
COPY content_web/*  /var/www/html/site/
COPY k8s/tls/* /etc/httpd/tls/
COPY confs/site.conf /etc/httpd/conf.d/

EXPOSE 80
EXPOSE 443

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh
CMD ["/run-httpd.sh"]
