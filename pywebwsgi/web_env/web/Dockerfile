FROM httpd:2.4.41

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY sources.list /etc/apt/

RUN apt update&& apt install -y gcc make python3 python3-dev python3-pip wget

WORKDIR /opt
RUN wget https://github.com/GrahamDumpleton/mod_wsgi/archive/4.7.1.tar.gz
RUN tar -xzvf 4.7.1.tar.gz
WORKDIR /opt/mod_wsgi-4.7.1
RUN ./configure --with-apxs=/usr/local/apache2/bin/apxs --with-python=/usr/bin/python3
RUN make&&make install

RUN echo 'LoadModule wsgi_module modules/mod_wsgi.so' >> /usr/local/apache2/conf/httpd.conf
RUN echo 'WSGIScriptAlias /myapp /opt/webapp/wsgi.py' >> /usr/local/apache2/conf/httpd.conf
RUN echo '<Directory /opt/webapp>' >> /usr/local/apache2/conf/httpd.conf
RUN echo 'Require all granted' >> /usr/local/apache2/conf/httpd.conf
RUN echo '</Directory>' >> /usr/local/apache2/conf/httpd.conf