FROM php:7.2-rc-zts
LABEL maintainer "Tony Blyler <me@tonyblyler.com>"

# FIXME get xdebug working for PHP 7.2 (not officially supported yet)
# pecl install xdebug
RUN apt-get update && \
	apt-get install -y \
		git \
		wget \
		openssh-client && \
	# pthreads install since pecl seems jacked up
	git clone --depth=1 https://github.com/krakjoe/pthreads -b master /tmp/pthreads && \
		cd /tmp/pthreads && \
		phpize && \
		./configure && \
		make && \
		make install && \
		cd - && \
		rm -Rf /tmp/pthreads && \
	docker-php-ext-install pcntl sockets && \
	docker-php-ext-enable pthreads
	# docker-php-ext-enable xdebug

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["php", "-a"]
