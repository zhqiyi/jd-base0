FROM node:lts-alpine
ARG JD_SHELL_URL=https://hub.fastgit.org/DX3242/jd-base0
ARG JD_SHELL_BRANCH=main
ARG JD_SCRIPTS_URL=https://gitee.com/ZFeng3242/JD-haoyangmao
ARG JD_SCRIPTS_BRANCH=main
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LANG=zh_CN.UTF-8 \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    JD_DIR=/jd \
    ENABLE_HANGUP=true \
    ENABLE_WEB_PANEL=true 
WORKDIR $JD_DIR
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update -f \
    && apk upgrade \
    && apk --no-cache add -f bash \
                             coreutils \
                             git \
                             wget \
                             curl \
                             nano \
                             tzdata \
                             perl \
                             openssh-client \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && git clone -b $JD_SHELL_BRANCH $JD_SHELL_URL $JD_DIR \
    && cd $JD_DIR/panel \
    && npm install \
    && git clone -b $JD_SCRIPTS_BRANCH $JD_SCRIPTS_URL $JD_DIR/scripts \
    && cd $JD_DIR/scripts \
    && npm install \
    && npm install -g pm2 \
    && ln -sf $JD_DIR/jd.sh /usr/local/bin/jd \
    && ln -sf $JD_DIR/jd.sh /usr/local/bin/task \
    && ln -sf $JD_DIR/git_pull.sh /usr/local/bin/git_pull \
    && ln -sf $JD_DIR/git_pull.sh /usr/local/bin/update \
    && ln -sf $JD_DIR/rm_log.sh /usr/local/bin/rm_log \
    && ln -sf $JD_DIR/rm_log.sh /usr/local/bin/rmlog \
    && ln -sf $JD_DIR/export_sharecodes.sh /usr/local/bin/export_sharecodes \
    && ln -sf $JD_DIR/export_sharecodes.sh /usr/local/bin/codes \
    && ln -sf $JD_DIR/csv.sh /usr/local/bin/csv \
    && cp -f $JD_DIR/docker/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh \
    && chmod 777 /usr/local/bin/docker-entrypoint.sh \
    && chmod 777 $JD_DIR/*.sh \
    && rm -rf /root/.npm
ENTRYPOINT ["docker-entrypoint.sh"]