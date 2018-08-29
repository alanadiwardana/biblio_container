FROM centos:centos7.5.1804

LABEL Vendor="CentOS" \
      License=GPLv2 \
      Version=2.4.6-40

RUN yum -y --setopt=tsflags=nodocs install epel-release && \
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

RUN yum -y --setopt=tsflags=nodocs update updateinfo yum-security
RUN yum -y --setopt=tsflags=nodocs install httpd
RUN yum -y --setopt=tsflags=nodocs install httpd-tools apr apr-util
RUN yum -y --setopt=tsflags=nodocs install php56w
RUN yum -y --setopt=tsflags=nodocs install php56w-xml php56w-xmlrpc php56w-soap php56w-gd php56w-mbstring
RUN yum -y --setopt=tsflags=nodocs install php56w-mysqlnd
RUN  yum -y --setopt=tsflags=nodocs install mod_ssl

EXPOSE 80
EXPOSE 443

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

# Our apache volume
VOLUME /var/www/html

CMD ["/run-httpd.sh"]

#sed -i -e 's/SSLMutex/Mutex/g' /etc/httpd/conf.d/ssl.conf
