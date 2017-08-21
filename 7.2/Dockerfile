FROM php:7.2-rc-zts
LABEL maintainer "Tony Blyler <me@tonyblyler.com>"

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
	# xdebug install since pecl doesn't like php 7.2 yet for xdebug
	git clone --depth=1 https://github.com/xdebug/xdebug -b master /tmp/xdebug && \
		cd /tmp/xdebug && \
		phpize && \
		./configure && \
		make && \
		make install && \
		cd - && \
		rm -Rf /tmp/xdebug && \
	docker-php-ext-install pcntl sockets && \
	docker-php-ext-enable pthreads xdebug

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["php", "-a"]
