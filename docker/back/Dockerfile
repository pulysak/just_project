FROM python:3

ARG DB_NAME
ARG DB_USER
ARG DB_PASSWORD

WORKDIR /usr/src/app
COPY just_project/ ./
COPY docker/* /docker/

RUN apt-get update && apt-get install -y postgresql-client && \

    mkdir -p /etc/uwsgi && \
    cp /docker/uwsgi.ini /etc/uwsgi && \
    cp /docker/requirements.txt /usr/src/app && \
    /docker/project_settings.ini.sh > /etc/project_settings.ini && \
    cat /etc/project_settings.ini && \
    pip install --no-cache-dir -r requirements.txt && \
    python manage.py collectstatic --noinput

CMD uwsgi --ini /etc/uwsgi/uwsgi.ini