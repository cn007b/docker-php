## PHP for DEVELOPMENT.

[![Docker Build Status](https://img.shields.io/docker/build/cn007b/php.svg)](https://hub.docker.com/r/cn007b/php/)
[![Docker Automated build](https://img.shields.io/docker/automated/cn007b/php.svg)](https://hub.docker.com/r/cn007b/php/)
[![Docker Pulls](https://img.shields.io/docker/pulls/cn007b/php.svg)](https://hub.docker.com/r/cn007b/php/)

Create test script with purpose to check docker commands:

```bash
echo '<?php var_dump("It works!");' > index.php
```

# CLI:

```bash
docker run -it --rm -v $PWD:/app -w /app cn007b/php php index.php
```
# CLI + Xdebug:

```bash
docker run -it --rm -v $PWD:/app -w /app -e PHP_IDE_CONFIG='serverName=docker' \
  cn007b/php php index.php
```

# Composer:

```bash
docker run -it --rm cn007b/php composer
```

# Protocol Buffers (ptotobuf):

```bash
docker run -it --rm cn007b/php protoc --version
```

# Built-in web server:

```bash
docker run -it --rm -v $PWD:/app -w /app -p 80:80 \
  cn007b/php php -S 0.0.0.0:80 index.php
```

Now open in browser [localhost](http://localhost:80/).

# Nginx:

```bash
docker run -it --rm -v $PWD:/app -w /app -p 80:80 cn007b/php /bin/bash -c '
    service php7.1-fpm start;
    service nginx start;
    tail -f /dev/stdout
  '
```

Now open in browser [localhost/index.php](http://localhost:80/index.php).

Add to end of URL [?XDEBUG_SESSION_START=PHPSTORM](http://localhost:80/index.php?XDEBUG_SESSION_START=PHPSTORM) with purpose to use Xdebug.

# Nginx with custom config:

```bash
docker run -it --rm -v $PWD:/app -w /app -p 80:80 \
  -v $PWD/nginx.default.conf:/etc/nginx/conf.d/default.conf \
  cn007b/php /bin/bash -c '
    service php7.1-fpm start;
    service nginx start;
    tail -f /dev/stdout
  '
```

# Configure Xdebug:

Set debug port in your IDE to `9002` and create IP alias `10.254.254.254` to your host machine,
for `OSX` use: `sudo ifconfig lo0 alias 10.254.254.254`,
for `Ubuntu` use: `sudo ifconfig lo 10.254.254.254 up`.
