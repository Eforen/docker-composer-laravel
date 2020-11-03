FROM php:7.4.12-fpm-buster

ARG USER_ID
ARG GROUP_ID
RUN cat /etc/passwd | grep "www-data" && ls -n /home
RUN cat /etc/passwd | grep "www-data" && echo "www-data is in passwd" || echo "www-data not in passwd"
RUN cat /etc/passwd | grep "1000" && echo "user 1000 may be in passwd" || echo "user 1000 not in passwd"
RUN cat /etc/group | grep "1000" && echo "group 1000 may be in passwd" || echo "group 1000 not in passwd"

RUN if [ ${USER_ID:-0} -ne 0 ] && [ ${GROUP_ID:-0} -ne 0 ]; then \
    userdel -f www-data &&\
    if getent group www-data ; then groupdel www-data; fi &&\
    groupadd -g ${GROUP_ID} www-data &&\
    useradd -l -u ${USER_ID} -g www-data www-data &&\
    install -d -m 0755 -o www-data -g www-data /home/www-data &&\
    chown -Rv --changes \
        --from=33:33 ${USER_ID}:${GROUP_ID} \
        /home \
        /etc \
        /var \
        /opt \
;fi

RUN cat /etc/passwd | grep "www-data" && ls -n /home
RUN cat /etc/passwd | grep "www-data" && echo "www-data is in passwd" || echo "www-data not in passwd"
RUN cat /etc/passwd | grep "1000" && echo "user 1000 may be in passwd" || echo "user 1000 not in passwd"
RUN cat /etc/group | grep "1000" && echo "group 1000 may be in passwd" || echo "group 1000 not in passwd"

RUN docker-php-ext-install pdo pdo_mysql

USER www-data

WORKDIR /var/www/html