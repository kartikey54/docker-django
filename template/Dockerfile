FROM python:{{PYTHON_VERSION}}

EXPOSE 8000

ENV GUNICORN_VERSION={{GUNICORN_VERSION}}
ENV DJANGO_VERSION={{DJANGO_VERSION}}
ENV PYTZ_VERSION={{PYTZ_VERSION}}

# create directory which can be a place for generated static content
# volume can be used to serve these files with a webserver
RUN mkdir -p /var/www/static
VOLUME /var/www/static

# create directory for application source code
# volume can be used for live-reload during development
RUN mkdir -p /usr/django/app
VOLUME /usr/django/app

# add gunicorn config
RUN mkdir -p /etc/gunicorn
COPY gunicorn.conf /etc/gunicorn/

# install gunicorn, django and pytz
RUN pip install gunicorn==$GUNICORN_VERSION
RUN pip install django==$DJANGO_VERSION
RUN pip install pytz==$PYTZ_VERSION

# run start.sh on container start
COPY start.sh /usr/django/
WORKDIR /usr/django
CMD bash start.sh
