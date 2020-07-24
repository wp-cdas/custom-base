FROM rocker/tidyverse:3.6.1

RUN R -e "install.packages('rtweet')"
RUN apt update && \
    apt install -y cron

COPY ./files/custom-cron /etc/cron.d/custom-cron

RUN chmod 0644 /etc/cron.d/custom-cron

RUN crontab /etc/cron.d/custom-cron    

RUN rm -f /etc/localtime && \
    ln -s /usr/share/zoneinfo/US/Eastern /etc/localtime

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

# Run the command on container startup
CMD cron && tail -f /var/log/cron.log
