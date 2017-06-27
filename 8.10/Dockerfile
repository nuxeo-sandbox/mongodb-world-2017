FROM nuxeo/nuxeo:8.10

# Notes:
#   Can use COPY command to install files from local system to the container, e.g. to install a patch jar

# Use root to perform build steps
USER root

ARG DEBIAN_FRONTEND=noninteractive

# Install wkhtmltopdf
RUN apt-get update && apt-get install wkhtmltopdf -y --no-install-recommends

# Add ffmpeg-support with MP4 support
# Add the nuxeo repository to the repository list
RUN echo "deb http://apt.nuxeo.org/ trusty releases" > /etc/apt/sources.list.d/nuxeo.list
# Register the nuxeo key
RUN wget -q -O- http://apt.nuxeo.org/nuxeo.key | apt-key add -
# Install ffmpeg-nuxeo
RUN apt-get update \
 && apt-get install ffmpeg-nuxeo

# Build Add ffmpeg-support with MP4 support from source
# RUN echo "deb http://deb.debian.org/debian jessie contrib non-free" >> /etc/apt/sources.list
# RUN apt-get update && apt-get install -y --no-install-recommends libfaac-dev git
# Build ffmpeg
# WORKDIR /tmp
# ENV BUILD_YASM true
# ENV LIBFAAC true
# RUN git clone https://github.com/nuxeo/ffmpeg-nuxeo.git
# WORKDIR ffmpeg-nuxeo
# RUN ./build-all.sh \
#  && cd /tmp \
#  && rm -Rf ffmpeg-nuxeo \
#  && rm -rf /var/lib/apt/lists/*

# Use Oracle JVM
# Inspired by http://www.webupd8.org/2014/03/how-to-install-oracle-java-8-in-debian.html
RUN apt-get remove -y --purge openjdk-8-jdk \
 && echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list \
 && echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list \
 && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 \
 && apt-get update \
 && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections \
 && apt-get install -y oracle-java8-installer \
 && apt-get install -y oracle-java8-set-default \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /var/cache/oracle-jdk8-installer

USER 1000
