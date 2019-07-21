
FROM php:5.5-apache

# Install PHP extension dependencies (if any)
#RUN apt-get update \
#    && apt-get -y --no-install-recommends install <package_name>

RUN echo "America/Sao_Paulo" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# Copy PHP configuration
# Edit docker/php.ini and customize it to your needs
COPY php.ini /usr/local/etc/php/conf.d/dev.ini

# Copy custom command docker-php-pecl-install
COPY docker-php-pecl-install /usr/local/bin/

# Install PHP extensions
RUN docker-php-ext-install mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

# Install PECL extensions
# RUN docker-php-pecl-install <package_name-version> (versions available in PECL repository allowed)
# RUN docker-php-pecl-install mdb2

# If you are using XDebug, this might be useful, if not, ignore it
# You additionally will have to customize docker/xdebug-ini-overrides.ini file to your needs
RUN docker-php-pecl-install xdebug-2.5.4
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Configure Apache VHOSTS
COPY app.conf /etc/apache2/sites-available/000-default.conf

ARG APACHE_SERVER_NAME

RUN sed -i "s/SERVER_NAME/${APACHE_SERVER_NAME}/g" /etc/apache2/sites-available/000-default.conf
RUN sed -i "s/WORK_DIR/${WORK_DIR}/g" /etc/apache2/sites-available/000-default.conf

RUN a2ensite 000-default.conf

# Activate Apache modules
#RUN a2enmod <module_name>
#RUN service apache2 restart
RUN a2enmod rewrite
RUN service apache2 restart

# Set the workdir
ARG WORK_DIR
WORKDIR ${WORK_DIR}

EXPOSE 80