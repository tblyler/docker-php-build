FROM php:7.2-rc-zts
LABEL maintainer "Tony Blyler <me@tonyblyler.com>"

# FIXME get xdebug working for PHP 7.2 (not officially supported yet)
# pecl install xdebug
RUN pecl install pthreads && \
	docker-php-ext-install pcntl sockets && \
	docker-php-ext-enable pthreads && \
	# docker-php-ext-enable xdebug && \
	apt-get update && \
	apt-get install -y \
		git \
		wget \
		openssh-client

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["php", "-a"]
