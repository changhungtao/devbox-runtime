FROM ghcr.io/labring-actions/devbox/debian-ssh-12.6:547a61

RUN cd /home/devbox/project && \
rm -rf ./*

COPY /Service/mcp/spring-boot-3-3-2/project /home/devbox/project

RUN apt-get update && \
    apt-get install -y wget && \
    wget https://download.java.net/openjdk/jdk17/ri/openjdk-17+35_linux-x64_bin.tar.gz && \
    mkdir /usr/lib/jvm && \
    tar -xvf openjdk-17+35_linux-x64_bin.tar.gz -C /usr/lib/jvm && \
    mv /usr/lib/jvm/jdk-17 /usr/lib/jvm/java-17-openjdk-amd64 && \
    rm openjdk-17+35_linux-x64_bin.tar.gz && \
    curl -o /tmp/apache-maven-3.8.6-bin.tar.gz https://archive.apache.org/dist/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz && \
    mkdir -p /opt/maven && \
    tar -xzf /tmp/apache-maven-3.8.6-bin.tar.gz -C /opt/maven && \
    ln -s /opt/maven/apache-maven-3.8.6 /opt/maven/latest && \
    ln -s /opt/maven/latest/bin/mvn /usr/bin/mvn && \
    rm /tmp/apache-maven-3.8.6-bin.tar.gz && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo 'export PATH=$PATH:$JAVA_HOME/bin' >> /home/devbox/.bashrc && \
    echo 'export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64' >> /home/devbox/.bashrc && \
    chown -R devbox:devbox /home/devbox/project && \
    chmod -R u+rw /home/devbox/project && \
    chmod -R +x /home/devbox/project/entrypoint.sh

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$PATH:$JAVA_HOME/bin
RUN mkdir /root/.devbox

USER devbox
RUN cd /home/devbox/project && \
    mvn install

