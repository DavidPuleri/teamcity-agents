FROM jetbrains/teamcity-agent

ENV DEBIAN_FRONTEND noninteractive

USER root

RUN apt-get update \
    && apt-get install -y software-properties-common \
        wget \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update -qq \
    && apt-get install -y php7.4-cli php-pear php7.4-curl php7.4-dev \
        php7.4-gd php7.4-mbstring php7.4-zip php7.4-mysql php7.4-xml php7.4-intl

RUN rm -rf /var/lib/apt/lists/* \
    && cd ~ \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"


RUN composer global require "phpunit/phpunit"
RUN ln -s ~/.composer/vendor/bin/phpunit /usr/local/bin/phpunit

RUN composer global require 'phpunit/dbunit=*'
RUN composer global require 'phpunit/php-invoker=*'
RUN composer global require 'phpunit/phpunit-selenium=*'
RUN composer global require phpmd/phpmd && ln -s ~/.composer/vendor/bin/phpmd /usr/local/bin/phpmd
RUN composer global require pdepend/pdepend && ln -s ~/.composer/vendor/bin/pdepend /usr/local/bin/pdepend
#RUN composer global require mayflower/php-codebrowser && ln -s ~/.composer/vendor/bin/phpcb /usr/local/bin/phpcb
RUN composer global require sebastian/phpcpd && ln -s ~/.composer/vendor/bin/phpcpd /usr/local/bin/phpcpd
RUN composer global require phploc/phploc && ln -s ~/.composer/vendor/bin/phploc /usr/local/bin/phploc
RUN composer global require squizlabs/php_codesniffer && ln -s ~/.composer/vendor/bin/phpcs /usr/local/bin/phpcs

#RUN curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

#RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
#RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install yarn
RUN npm install -g bower

RUN npm install phantomjs@1.9.20
RUN ln -s /node_modules/phantomjs/lib/phantom/bin/phantomjs /usr/local/bin/phantomjs

RUN npm install -g semver

RUN apt-get install -y openjdk-11-jdk
