FROM python:3.9.5-slim-buster

LABEL maintainer="Julien Pierini <julien.pierini@ekino.com>"

ARG TERRAFORM_VERSION
ARG TERRAGRUNT_VERSION
ARG TERRAFORM_COMPLIANCE_VERSION
ARG INFRACOST_VERSION
ARG AZURE_CLI_VERSION

RUN apt-get update -qq \
    && apt-get -y -qq install unzip wget git jq bc \
    && pip install -U pip \
    && pip install awscli boto3 pipenv terraform-compliance==$TERRAFORM_COMPLIANCE_VERSION azure-cli==${AZURE_CLI_VERSION} \
    && wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -O terraform.zip \
    && unzip -o terraform.zip \
    && rm terraform.zip \
    && mv terraform /usr/bin/ \
    && chmod +x /usr/bin/terraform

RUN wget https://github.com/gruntwork-io/terragrunt/releases/download/v${TERRAGRUNT_VERSION}/terragrunt_linux_amd64 -O terragrunt \
    && mv terragrunt /usr/bin \
    && chmod +x /usr/bin/terragrunt

RUN wget https://github.com/infracost/infracost/releases/download/v${INFRACOST_VERSION}/infracost-linux-amd64.tar.gz -O infracost.tar.gz \
    && tar xvf infracost.tar.gz \
    && mv infracost-linux-amd64 /usr/bin/infracost

RUN wget https://raw.githubusercontent.com/infracost/infracost/v${INFRACOST_VERSION}/scripts/ci/diff.sh -O /opt/diff.sh \
    && chmod +x /opt/diff.sh
