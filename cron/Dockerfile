FROM sipcapture/homer-webapp
MAINTAINER L. Mangani <lorenzo.mangani@gmail.com>
ENV BUILD_DATE 2017-05-18

# Install the cron service
RUN touch /var/log/cron.log
RUN apt-get update -qq && apt-get install cron mysql-client -y && rm -rf /var/lib/apt/lists/*

# Add our crontab file
COPY homer_mysql_rotate.pl /opt/mysql/homer_mysql_rotate.pl

RUN echo "30 3 * * * /opt/mysql/homer_mysql_rotate >> /var/log/cron.log 2>&1" > /crons.conf
RUN crontab /crons.conf

COPY rotation.ini /opt/mysql/rotation.ini

COPY run.sh /run.sh
RUN chmod a+rx /run.sh

ENTRYPOINT ["/run.sh"]
