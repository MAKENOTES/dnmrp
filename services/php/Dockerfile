#FROM makenotes/apline_php74:1.0
FROM makenotes/apline_php72:1.5

# Install composer and change it's cache home
RUN curl -o /usr/bin/composer https://mirrors.aliyun.com/composer/composer.phar \
    && chmod +x /usr/bin/composer
ENV COMPOSER_HOME=/tmp/composer

# 字体 - 宋体
ADD fonts/simsun.ttc  /usr/share/fonts/simsun.ttc
ADD fonts/simsun.ttf /usr/share/fonts/simsun.ttf
# 安装 wkhtmltopdf
ADD wkhtmltopdf/wkhtmltopdf /usr/bin/wkhtmltopdf
RUN chmod 755 /usr/bin/wkhtmltopdf
# 添加 wkhtmltopdf 启动脚本
ADD wkhtmltopdf/startup /usr/bin/startup
RUN chmod 755 /usr/bin/startup

# php image's www-data user uid & gid are 82, change them to 1000 (primary user)
RUN apk --no-cache add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data

WORKDIR /var/www
