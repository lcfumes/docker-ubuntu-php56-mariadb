FROM ubuntu:15.10
MAINTAINER Luiz Fumes <lcfumes@gmail.com>

#Update and Intalation Ubuntu Packages
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y nginx
RUN apt-get install -y php5 php5-cli php5-common php5-curl php5-fpm php5-mysql php5-intl php-pear php5-imap php5-mcrypt php5-memcache php5-gd

# Nginx config
#Add Files
ADD nginx.conf /etc/nginx/nginx.conf
ADD web.conf /etc/nginx/sites-available/webserver.conf
ADD .bashrc /root/.bashrc

#Create a symbolic link to avaliable sites
RUN ln -s /etc/nginx/sites-available/webserver.conf /etc/nginx/sites-enabled/webserver.conf

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

#php-fpm config
RUN sed -i "s/;date.timezone =/date.timezone = America\/Sao_Paulo/" /etc/php5/fpm/php.ini 
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini
RUN sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php5/fpm/pool.d/www.conf

#Commands
CMD service php5-fpm start && nginx

#Port
EXPOSE 80
