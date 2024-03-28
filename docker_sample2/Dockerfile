FROM ubuntu

# アップデート
RUN apt-get update

# apache2, python, mod-wsgiをインストールする
RUN apt-get install -y apt-utils vim curl apache2 apache2-utils apache2-dev
RUN apt-get -y install python3 libapache2-mod-wsgi-py3
RUN ln /usr/bin/python3 /usr/bin/python
RUN apt-get -y install python3-pip

# pythonにdjangoをインストールする
RUN pip install --upgrade pip
RUN pip install django ptvsd

# pythonにmod-wsgiをインストールする
RUN pip install mod_wsgi mod-wsgi-httpd

# apacheの設定ファイルにmod-wsgiの設定を追加
COPY ./apache_django.conf /etc/apache2/sites-available/apache_django.conf
RUN a2ensite apache_django.conf

# Djangoソースコードをマウント
VOLUME ./web/mysite ./var/web/mysite

EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]



