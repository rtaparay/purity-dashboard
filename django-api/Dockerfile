FROM python:3.9.6-alpine

WORKDIR /usr/src/app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apk upgrade && apk update \
  && apk add --virtual build-deps gcc python3-dev musl-dev \
  && apk add postgresql \
  && apk add postgresql-dev \
  && apk add gcc \
  && pip install psycopg2 \
  && apk add jpeg-dev zlib-dev libjpeg \
  && pip install Pillow \
  && apk del build-deps

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy entrypoint.sh
COPY ./entrypoint.sh .
RUN sed -i 's/\r$//g' /usr/src/app/entrypoint.sh
RUN chmod +x /usr/src/app/entrypoint.sh

# copy project
COPY . .

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]