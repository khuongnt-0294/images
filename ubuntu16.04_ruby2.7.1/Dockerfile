iFROM ubuntu:16.04
MAINTAINER KhuongNT

RUN apt-get update \
  && apt-get install -y \
      curl \
      autoconf \
      automake \
      bison \
      gawk \
      sqlite3 \
      make \
      imagemagick \
      libbz2-dev \
      libcurl4-openssl-dev \
      libevent-dev \
      libffi-dev \
      libgdbm-dev \
      libglib2.0-dev \
      libgmp-dev \
      libjpeg-dev \
      libmagickcore-dev \
      libmagickwand-dev \
      libmysqlclient-dev \
      libncurses-dev \
      libpq-dev \
      libreadline-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libxslt-dev \
      libyaml-dev \
      zlib1g-dev \
      sudo \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - && apt-get install -y nodejs
RUN apt-get install -y openssh-client openssh-server
RUN apt-get install -y git-core build-essential libxslt1-dev vim software-properties-common
RUN apt-get install -y qt5-default libbison-dev libqt5webkit5-dev mysql-client
RUN npm install -g yarn
RUN apt-get install -y tzdata

# Add user deploy
RUN useradd -m deploy && echo "deploy:deploy" | chpasswd && adduser deploy sudo
#RUN useradd -m -d /home/deploy -s /bin/bash -g deploy deploy 
RUN echo "deploy:deploy" | chpasswd \
 && mkdir /home/deploy/.ssh \
 && chmod 700 /home/deploy/.ssh \
 && chown -R deploy:deploy /home/deploy/
RUN mkdir /usr/local/rails_apps && chown -R deploy:deploy /usr/local/

RUN echo "deploy ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN echo "Defaults        exempt_group=wheel" >> /etc/sudoers
WORKDIR /home/deploy

# Install RVM
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys \
  409B6B1796C275462A1703113804BB82D39DC0E3 \
  7D2BAF1CF37B13E2069D6956105BD0E739499BDB \
  && curl -sSL https://get.rvm.io | bash -s -- --autolibs=read-fail stable
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN /bin/bash -l -c "rvm requirements"
RUN /bin/bash -l -c "rvm install 2.7.1"
RUN /bin/bash -l -c "gem install bundler"
RUN \touch .bashrc
RUN echo 'source /usr/local/rvm/scripts/rvm' > .bashrc

USER deploy

