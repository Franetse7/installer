#
# Copyright (c) .NET Foundation and contributors. All rights reserved.
# Licensed under the MIT license. See LICENSE file in the project root for full license information.
#

# Dockerfile that creates a container suitable to build dotnet-cli
FROM mcr.microsoft.com/dotnet-buildtools/prereqs:rhel-7-rpmpkg-e1b4a89-20175311035359

# Setup User to match Host User, and give superuser permissions
ARG USER_ID=0
RUN useradd -m code_executor -u ${USER_ID} -g root
RUN echo 'code_executor ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# With the User Change, we need to change permissions on these directories
RUN chmod -R a+rwx /usr/local
RUN chmod -R a+rwx /home
RUN chown root:root /usr/bin/sudo && chmod 4755 /usr/bin/sudo

# Set user to the one we just created
USER ${USER_ID}

# Set working directory
ARG WORK_DIR
WORKDIR ${WORK_DIR}

# Set up Azure Artifacts credential provider
RUN wget -qO- https://raw.githubusercontent.com/Microsoft/artifacts-credprovider/master/helpers/installcredprovider.sh | bash
