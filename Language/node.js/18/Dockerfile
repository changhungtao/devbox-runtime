FROM ghcr.io/labring-actions/devbox/debian-ssh-12.6:547a61

RUN cd /home/devbox/project && \
rm -rf ./*

USER devbox
ENV NODE_VERSION 18
ENV NVM_DIR /home/devbox/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash \
    && . $NVM_DIR/nvm.sh 

USER root
COPY /Language/node.js/project /home/devbox/project
 
RUN apt-get update && \
    apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g typescript yarn pnpm && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    chown -R devbox:devbox /home/devbox/project && \
    chmod -R u+rw /home/devbox/project && \
    chmod -R +x /home/devbox/project/entrypoint.sh
USER devbox
 
RUN mkdir -p /home/devbox/.devbox