FROM laradock/workspace:2.2-7.2

RUN DEBIAN_FRONTEND=noninteractive

USER root

###########################################################################
# Laradock non-root user:
###########################################################################

# Add a non-root user to prevent files being created with root permissions on host machine.
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

# always run apt update when start and after add new source list, then clean up at end.
RUN apt-get update -yqq && \
  pecl channel-update pecl.php.net && \
  groupadd -g ${PGID} laradock && \
  useradd -u ${PUID} -g laradock -m laradock -G docker_env && \
  usermod -p "*" laradock

###########################################################################
# Set Timezone
###########################################################################

ARG TZ=UTC
ENV TZ ${TZ}

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#
USER root

# Clean up
RUN apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
  rm /var/log/lastlog /var/log/faillog

# Set default work directory
WORKDIR /var/www
