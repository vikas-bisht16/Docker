FROM ubuntu:18.04
ARG  APPSERVER_ENDPOINT
ARG  DB_ENDPOINT
RUN  apt-get update -y
RUN  apt-get install python-pip -y
RUN  pip install --upgrade setuptools
RUN  easy_install -U setuptools || true
RUN  python -m pip install --upgrade pip
RUN  pip install pymysql
RUN  apt-get install git apache2 -y
RUN mkdir devops_test
RUN  git clone https://gitlab.com/crest1/devops_test.git /tmp/devops_test
RUN  sed -i "s/appserver.company.com/${APPSERVER_ENDPOINT}/g" /tmp/devops_test/mtwa.conf
RUN  sed -i "s/dbserver.company.com/${DB_ENDPOINT}/g" /tmp/devops_test/mtwa.conf
RUN  a2dismod mpm_event || true
RUN  a2enmod mpm_prefork cgi || true
RUN  apt-get install sudo wget -y
RUN  wget "https://s3.amazonaws.com/richbourg-s3/mtwa/web/000-default.conf" -P /tmp/
RUN  wget "https://s3.amazonaws.com/richbourg-s3/mtwa/web/ports.conf" -P /tmp
RUN  cp /tmp/000-default.conf /etc/apache2/sites-enabled/
RUN  cp /tmp/ports.conf /etc/apache2/
RUN mkdir /etc/mtwa
RUN mkdir /var/www/html/appdemo
RUN cp /tmp/devops_test/mtwa.conf /etc/mtwa/mtwa.conf
RUN cp /tmp/devops_test/html/* /var/www/html/appdemo/
RUN cp /tmp/devops_test/scripts/* /var/www/html/appdemo/
EXPOSE 80
ENTRYPOINT ["apachectl", "-D", "FOREGROUND"]