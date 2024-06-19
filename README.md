# Flask Boilerplate

### Prerequisites

- Python 3.11.3 or higher
- Up and running Redis client

### Project setup
```sh
# clone the repo
$ git clone https://github.com/vallettasoftware/flask-boilerplate.git
# move to the project folder
$ cd flask-boilerplate
```
If you want to install redis via docker
```sh
$ docker run -d --rm --name redis_py -p6379:6379 redis
```

### Creating virtual environment

- Install `pipenv` a global python project `pip install pipenv --user`
- Create a `virtual environment` for this project
```shell
# creating pipenv environment for python 3
$ python -m pipenv --three
# activating the pipenv environment
$ python -m pipenv shell
# install all dependencies (include -d for installing dev dependencies)
$ python -m pipenv install -d

# if you have multiple python 3 versions installed then
$ python -m pipenv install -d --python 3.12
```
### Configuration

- There are 3 configurations `development`, `staging` and `production` in `config.py`. Default is `development`
- Create a `.env` file from `.env.example` and set appropriate environment variables before running the project

### Running app

- Run flask app `python run.py`
- Logs would be generated under `log` folder

### Running celery workers

- Run redis locally before running celery worker
- Celery worker can be started with following command
```sh
# run following command in a separate terminal
$ celery -A celery_worker.celery worker --loglevel='INFO'  
# (append `--pool=solo` for windows)
```


# Preconfigured Packages
Includes preconfigured packages to kick start flask app by just setting appropriate configuration.

| Package 	| Usage 	|
|-----	|-----	|
| [celery](https://docs.celeryproject.org/en/stable/getting-started/introduction.html) 	| Running background tasks 	|
| [redis](https://redislabs.com/lp/python-redis/) 	| A Python Redis client for caching 	|
| [flask-cors](https://flask-cors.readthedocs.io/) 	| Configuring CORS 	|
| [python-dotenv](https://pypi.org/project/python-dotenv/) 	| Reads the key-value pair from .env file and adds them to environment variable. 	|
| [marshmallow](https://marshmallow.readthedocs.io/en/stable/) 	| A package for creating Schema, serialization, deserialization 	|
| [webargs](https://webargs.readthedocs.io/) 	| A Python library for parsing and validating HTTP request objects 	|

`autopep8` & `flake8` as `dev` packages for `linting and formatting`

# Test
  Test if this app has been installed correctly and it is working via following curl commands (or use in Postman)
- Check if the app is running via `status` API
```shell
$ curl --location --request GET 'http://localhost:5000/status'
```
- Check if core app API and celery task is working via
```shell
$ curl --location --request GET 'http://localhost:5000/api/v1/core/test'
```
- Check if authorization is working via (change `API Key` as per you `.env`)
```shell
$ curl --location --request GET 'http://localhost:5000/api/v1/core/restricted' --header 'x-api-key: 436236939443955C11494D448451F'
```