FROM ubuntu:18.04

ARG HTTP_PROXY=${HTTP_PROXY}
ARG HTTPS_PROXY=${HTTPS_PROXY}

ENV http_proxy $HTTP_PROXY
ENV https_proxy $HTTPS_PROXY
ENV no_proxy $NO_PROXY

RUN apt-get update && apt-get install -y -qq apt-transport-https curl net-tools iproute2 \
 && echo "deb https://packages.wand.net.nz bionic ovs-2.10" >  /etc/apt/sources.list.d/ovs.list \
 && curl https://packages.wand.net.nz/keyring.gpg -o /etc/apt/trusted.gpg.d/wand.gpg \
 && apt-get update && apt install -y -qq ovn-common openvswitch-common openvswitch-switch


ENV OPERATOR=/usr/local/bin/nfn-operator \
    AGENT=/usr/local/bin/nfn-agent \
    USER_UID=1001 \
    USER_NAME=nfn-operator

# install operator binary
COPY bin/nfn-operator ${OPERATOR}

COPY bin /usr/local/bin

ENTRYPOINT ["/usr/local/bin/entrypoint"]
