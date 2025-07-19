# Dockerfile
FROM gitlab/gitlab-runner:alpine-v18.2.0 

# Install dependencies (you can switch to a Debian/Ubuntu base if needed)
RUN apk add --no-cache bash curl unzip openjdk11 tar git docker-cli gzip

# Install Helm
ENV HELM_VERSION="v3.14.4"

RUN curl -fsSL -o helm.tar.gz https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    tar -zxvf helm.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    chmod +x /usr/local/bin/helm && \
    rm -rf helm.tar.gz linux-amd64

ARG KUBECTL_VERSION="v1.29.0"

# Install kubectl
RUN apk add --no-cache curl && \
    curl -LO "https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Set environment variables
ENV WDT_VERSION=latest
ENV WDT_HOME=/opt/wdt

# Download and install WDT
RUN mkdir -p $WDT_HOME && \
    curl -L -o /tmp/weblogic-deploy.zip https://github.com/oracle/weblogic-deploy-tooling/releases/${WDT_VERSION}/download/weblogic-deploy.zip && \
    unzip /tmp/weblogic-deploy.zip -d $WDT_HOME && \
    rm /tmp/weblogic-deploy.zip

ENV PATH="$WDT_HOME:$PATH"
