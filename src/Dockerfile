FROM hashicorp/terraform:0.12.29
ARG OCTO_TOOLS_VERSION=7.4.1
ARG AZ_CLI_VERSION=2.9.1

RUN \
  apk update && \
  apk add --update curl && \
  apk add bash py-pip && \
  apk add --update --no-cache build-base python3-dev python3 libffi-dev libressl-dev bash git gettext curl && curl -O https://bootstrap.pypa.io/get-pip.py && python3 get-pip.py && \
  pip --no-cache-dir install -U pip && \
  pip --no-cache-dir install pip install dotnetcore2 && \
  pip --no-cache-dir install azure-cli==$AZ_CLI_VERSION && \  
  apk del --purge build-base 

RUN apk add --no-cache icu-libs
ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT false
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8



LABEL maintainer="runsyn@signicat.com" \
        signicat.dockerfile.version="1.0" \
        terraform.tools.version="0.12.29" \
        az.tools.version=AZ_CLI_VERSION \
        octopus.tools.version=$OCTO_TOOLS_VERSION


ENV OCTO_TOOLS_DOWNLOAD_URL https://download.octopusdeploy.com/octopus-tools/$OCTO_TOOLS_VERSION/OctopusTools.$OCTO_TOOLS_VERSION.portable.tar.gz


WORKDIR /octo
RUN curl ${OCTO_TOOLS_DOWNLOAD_URL}  --output OctopusTools.tar.gz && tar -zxvf OctopusTools.tar.gz

RUN apk del curl

WORKDIR /src
ENTRYPOINT ["dotnet", "/octo/Octo.dll"]