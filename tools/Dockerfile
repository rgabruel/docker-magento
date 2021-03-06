# PHP 5.4 with FPM and Magento dependencies
FROM debian:wheezy
MAINTAINER Michael A. Smith <msmith3@ebay.com>
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/root/.composer/vendor/bin
ADD https://github.com/phpDocumentor/phpDocumentor2/commit/315b5a78faf93350431efa16d94eb2ffb38abdc1.diff /tmp/issue-1460.patch
RUN apt-get update -qqy && \
    apt-get install -qqy \
            bzip2 \
            curl \
            git \
            graphviz \
            libxml2-utils \
            mysql-client \
            php-apc \
            php-soap \
            php5 \
            php5-curl \
            php5-gd \
            php5-mcrypt \
            php5-mysql \
            php5-xdebug \
            php5-xsl \
            vim \
            && \
    curl -Ss https://raw.githubusercontent.com/colinmollenhour/modman/master/modman > /usr/local/bin/modman && \
    curl -Ss https://getcomposer.org/composer.phar > /usr/local/bin/composer && \
    curl -Ss https://raw.githubusercontent.com/netz98/n98-magerun/master/n98-magerun.phar > /usr/local/bin/n98-magerun.phar && \
    chmod +x /usr/local/bin/composer /usr/local/bin/modman /usr/local/bin/n98-magerun.phar && \
    composer -qn --no-ansi global require pdepend/pdepend phpdocumentor/phpdocumentor phploc/phploc phpmd/phpmd phpunit/dbunit phpunit/php-invoker phpunit/phpunit-selenium phpunit/phpunit-story sebastian/phpcpd squizlabs/php_codesniffer && \
    cd /usr/local/bin && ln -s n98-magerun.phar n98-magerun && ln -s n98-magerun.phar magerun && \
    cd /root/.composer/vendor/phpdocumentor/phpdocumentor && patch -p1 < /tmp/issue-1460.patch && rm /tmp/issue-1460.patch
WORKDIR /srv/magento
COPY install /usr/local/bin/install_magento
