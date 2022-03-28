ARG MYSQL_VERSION
FROM mysql:${MYSQL_VERSION}

#####################################
# Set Timezone
#####################################

ARG TZ=PRC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && chown -R mysql:root /var/lib/mysql/

COPY my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod 0444 /etc/mysql/conf.d/my.cnf

EXPOSE 3306

CMD ["mysqld"]
