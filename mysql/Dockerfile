# FROM mysql:5.7.20
FROM openshift/mysql-55-centos7

ENV MYSQL_ALLOW_EMPTY_PASSWORD=yes \
    MYSQL_DATABASE=cities \
    MYSQL_USER=shipping \
    MYSQL_PASSWORD=secret

# change datadir entry in /etc/mysql/my.cnf
COPY config.sh /root/
RUN /root/config.sh

COPY scripts/* /docker-entrypoint-initdb.d/
RUN /entrypoint.sh mysqld & while [ ! -f /tmp/finished ]; do sleep 10; done
RUN rm /docker-entrypoint-initdb.d/*

#RUN chgrp -R 0 /data/mysql && \
#    chmod -R g=u /data/mysql

#RUN chgrp -R 0 /var/run && \
#    chmod -R g=u /var/run

# MOUNT /var/lib/mysql
RUN chgrp -R 0 /var/lib/mysql && \
    chmod -R g=u /var/lib/mysql

EXPOSE 3306
# USER 27

USER 1001
