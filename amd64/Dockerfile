FROM amazonlinux:latest

USER root

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN yum update -y \
&& yum install -y shadow-utils curl jq wget \
&& amazon-linux-extras install docker \
&& yum clean all \
&& rm -rf /var/cache/yum \
&& adduser --shell /bin/false --home /home/nopriv nopriv \
&& TRIVY_VERSION=$(curl -sL "https://api.github.com/repos/aquasecurity/trivy/releases/latest" | jq -r ".tag_name" | cut -c2-10) \
&& echo $TRIVY_VERSION \
&& wget -q "https://github.com/aquasecurity/trivy/releases/download/v${TRIVY_VERSION}/trivy_${TRIVY_VERSION}_Linux-64bit.rpm" \
&& yum install -y /trivy_${TRIVY_VERSION}_Linux-64bit.rpm

USER nopriv
