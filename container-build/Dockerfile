# Use the httpd-parent image as base
FROM quay.io/redhattraining/httpd-parent

# OpenShift specific requirements and best practice

#can't use ports below 1024: add some descriptive labels
EXPOSE 8080
LABEL io.k8s.description="A basic Apache HTTP Server child image; use ONBUILD" \
      io.k8s.display-name="Apache HTTP Server" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="apache, httpd"

# this actually edits (changes) the listening ports in the httpd config
# - and makes the Apache working directories accessible to group 'root'
RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf && \
    chgrp -R 0 /var/log/httpd /var/run/httpd && \
    chmod -R g=u /var/log/httpd /var/run/httpd
USER 1001
