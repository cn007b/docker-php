FROM cn007b/php:7.1

MAINTAINER Vladimir Kovpak <cn007b@gmail.com>

# php-protobuf
RUN pecl channel-update pecl.php.net \
    && pear install Console_CommandLine \
    && pear channel-discover pear.pollinimini.net \
    && pear install drslump/Protobuf-beta
