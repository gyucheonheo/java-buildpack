ARG base_image=ubuntu:bionic
FROM ${base_image}

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    libssl1.0-dev \
    libreadline-dev \
    lsb-release \
    locales \
    python \
    zip \
    zlib1g-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update -qqy \
	&& apt-get -qqy install wget libgtk-3-0 libx11-xcb1 libdbus-glib-1-2 libxt6 \
	&& rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
	&& wget -q -O /tmp/firefox.tar.bz2 https://download-installer.cdn.mozilla.net/pub/firefox/releases/$FIREFOX_VERSION/linux-x86_64/en-US/firefox-$FIREFOX_VERSION.tar.bz2 \
	&& tar xjf /tmp/firefox.tar.bz2 -C /opt \
	&& rm /tmp/firefox.tar.bz2 \
	&& mv /opt/firefox /opt/firefox-$FIREFOX_VERSION \
	&& ln -s /opt/firefox-$FIREFOX_VERSION/firefox /usr/bin/firefox \

RUN locale-gen en_US.UTF-8 \
 && /usr/sbin/update-locale LANG=en_US.UTF-8 \
 && dpkg-reconfigure -f noninteractive locales

RUN git clone https://github.com/rbenv/rbenv.git $HOME/.rbenv \
 && cd $HOME/.rbenv \
 && src/configure \
 && make -C src \
 && ln -s $HOME/.rbenv/bin/rbenv /usr/local/bin

RUN eval "$(rbenv init -)" \
 && git clone https://github.com/rbenv/ruby-build.git $(rbenv root)/plugins/ruby-build

RUN eval "$(rbenv init -)" \
 && git clone https://github.com/sstephenson/rbenv-default-gems.git $(rbenv root)/plugins/rbenv-default-gems \
 && echo 'bundler' >> $(rbenv root)/default-gems

RUN eval "$(rbenv init -)" \
 && rbenv install 2.5.8

RUN eval "$(rbenv init -)" \
 && rbenv install 2.6.6

RUN eval "$(rbenv init -)" \
 && rbenv install 2.7.1
