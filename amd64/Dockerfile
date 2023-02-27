FROM amazonlinux:latest

USER root

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN yum update -y \
&& yum install -y shadow-utils curl jq wget unzip \
&& curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
&& unzip -q awscliv2.zip \
&& ./aws/install \
&& rm -rf awscliv2.zip \
aws \
/usr/local/aws-cli/v2/*/dist/aws_completer \
/usr/local/aws-cli/v2/*/dist/awscli/data/ac.index \
/usr/local/aws-cli/v2/*/dist/awscli/examples \
&& yum clean all \
&& rm -rf /var/cache/yum \
&& adduser --shell /bin/false --home /home/nopriv nopriv \
&& TRIVY_VERSION=$(curl -sL "https://api.github.com/repos/aquasecurity/trivy/releases/latest" | jq -r ".tag_name" | cut -c2-10) \
&& echo $TRIVY_VERSION \
&& wget -q "https://github.com/aquasecurity/trivy/releases/download/v${TRIVY_VERSION}/trivy_${TRIVY_VERSION}_Linux-64bit.rpm" \
&& yum install -y /trivy_${TRIVY_VERSION}_Linux-64bit.rpm

USER nopriv
