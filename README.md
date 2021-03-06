# Simple Flask and Redis app using Docker Compose

This is a simple Flask app that keeps track of how many times you visit the website url. 


## Dockerfile

```python

FROM python:3.4-alpine

ADD . /code

WORKDIR /code

RUN pip install -r requirements.txt

CMD ["python", "app.py"]


```

This tells Docker to:

* Build an image starting with the Python 3.4 image.

* Add the current directory `.` into the path `/code` in the image.

* Set the working directory to `/code`.

* Install the Python dependencies.

* Set the default command for the container to `python app.py.


## Compose file

```python

version: '3'
services:
  web:
    build: .
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: "redis:alpine"


```

This Compose file defines two services, `web` and `redis`. The web service:

* Uses an image that’s built from the `Dockerfile` in the current directory.

* Forwards the exposed port 5000 on the container to port 5000 on the host machine. We use the default port for the Flask web server, `5000`.

* The volumes key mounts the project directory (current directory) on the host to /code inside the container, allowing you to modify the code on the fly, without having to rebuild the image.


## Build and run

To run the containers write:

```python

docker-compose up

```

And then visit http://localhost:5000


## Stop Docker

To stop a running service simply type CTRL + C

Afterward, to bring everything down and remove unused containers type:

```python

docker-compose down --volumes

```
