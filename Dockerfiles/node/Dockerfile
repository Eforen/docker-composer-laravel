FROM node:13.7

ARG USER_ID
ARG GROUP_ID

RUN cat /etc/passwd | grep "node" && ls -n /home
RUN cat /etc/passwd | grep "node" && echo "node is in passwd" || echo "node not in passwd"
RUN cat /etc/passwd | grep "1000" && echo "user 1000 may be in passwd" || echo "user 1000 not in passwd"
RUN cat /etc/group | grep "1000" && echo "group 1000 may be in passwd" || echo "group 1000 not in passwd"

RUN if [ ${USER_ID:-0} -ne 0 ] && [ ${GROUP_ID:-0} -ne 0 ]; then \
    userdel -f node &&\
    if getent group node ; then groupdel node; fi &&\
    groupadd -g ${GROUP_ID} node &&\
    useradd -l -u ${USER_ID} -g node node &&\
    install -d -m 0755 -o node -g node /home/node &&\
    chown -Rv --changes \
        --from=33:33 ${USER_ID}:${GROUP_ID} \
        /home \
        /etc \
        /var \
        /opt \
;fi

RUN cat /etc/passwd | grep "node" && ls -n /home
RUN cat /etc/passwd | grep "node" && echo "node is in passwd" || echo "node not in passwd"
RUN cat /etc/passwd | grep "1000" && echo "user 1000 may be in passwd" || echo "user 1000 not in passwd"
RUN cat /etc/group | grep "1000" && echo "group 1000 may be in passwd" || echo "group 1000 not in passwd"

USER node

WORKDIR /var/www/html