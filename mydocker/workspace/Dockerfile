FROM laradock/workspace:1.3
ARG PUID=1000
ARG PGID=1000
RUN groupadd -g $PGID laradock && \
    useradd -u $PUID -g laradock -m laradock

ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ARG INSTALL_WORKSPACE_SSH=false
ENV INSTALL_WORKSPACE_SSH ${INSTALL_WORKSPACE_SSH}


RUN if [ ${INSTALL_WORKSPACE_SSH} = true ]; then \
    rm -f /etc/service/sshd/down && \
    cat /tmp/id_rsa.pub >> /root/.ssh/authorized_keys \
        && cat /tmp/id_rsa.pub >> /root/.ssh/id_rsa.pub \
        && cat /tmp/id_rsa >> /root/.ssh/id_rsa \
        && rm -f /tmp/id_rsa* \
        && chmod 644 /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub \
    && chmod 400 /root/.ssh/id_rsa \
;fi

USER laradock

ARG INSTALL_DEPLOYER=false
ENV INSTALL_DEPLOYER ${INSTALL_DEPLOYER}

RUN if [ ${INSTALL_DEPLOYER} = true ]; then \
    # Install the Deployer
    composer global require "deployer/deployer" \
;fi



USER root
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set default work directory
WORKDIR /var/www
CMD ["composer", "install"]

