FROM ubuntu:21.04

ENV ANSIBLE_VERSION 2.10.5

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y openssh-client sshpass curl wget apt-transport-https lsb-release python3-pip git unzip; \
    apt-get autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip; \
    pip3 install "ansible==${ANSIBLE_VERSION}" ansible-lint pywinrm>=0.3.0 boto3; \
    wget -q https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt; \
    pip3 install -r requirements-azure.txt; \
    rm requirements-azure.txt; \
    ansible-galaxy collection install azure.azcollection community.aws; \
    curl -sL https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip -o awscliv2.zip; \
    unzip awscliv2.zip; \
    ./aws/install; \
    rm awscliv2.zip; \
    rm -Rf ./aws/; \
    curl -sL https://aka.ms/InstallAzureCLIDeb | bash

COPY .bashrc /root/.bashrc