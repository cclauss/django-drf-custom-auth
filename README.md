# Custom Authentication & Authorization in Django-DRF


## Tools & Services:
- Django & DRF : for building the APIs
- Docker & Docker compose: Containerization
- Celery: For running background task
- Rabbit MQ: A message broker for celery
- Flower dashboard: For monitoring celery background tasks
- PostgreSQL: Relational DB


## By the end of this tutorial 

- Create an API that allows an admin to create roles and assign permissions into the role.
- Create users and assign one or more roles to users.
- Use these roles and permissions to protect API endpoints so that only users with the appropriate permissions can access them
- Lock a user account after the maximum allowable failed attempts.

## Running locally

Create a .env file by copying the .env.sample provided and run:
```
docker compose build && docker compose up
```
to start the container. As an alternative, run:
```
docker compose -f docker-compose.dev.yml up --build
```
to build and run the container using the dev yaml file.
Make sure to externalize the db instance to be used. It can be in another container.

## Run tests
Run descriptive tests in the container using:
```
docker compose exec <docker_container_name> pytest -rP -vv
```

Access the docs on:

```
http://localhost:8000/api/v1/doc
```


## Running In a Virtual Env

Create a virtual environment using:
```
mkvirtualenv <env_name>
```

Ensure you have installed `virtualenv` on your system and install dev dependencies using
```
pip install -r app/requirements/dev.txt
```

Navigate to app directory and run migrations using:
```
python manage.py makemigrations

python manage.py migrate
```

Run the server using:
```
python manage.py runserver
```

#  Generating Fixtures (Seeding Permissions)

## Permissions

Load permissions needed in app into the db

```bash
python manage.py loaddata */fixtures/*.json
```

Export Permissions from db

```sh
python manage.py dumpdata  --format=json user.Permission -o core/fixtures/Permission.json
```


Access docs:
```sh
http://localhost:8000/api/v1/doc
```
![Screenshot](screenshot1.png)
<br><br><br>
![Screenshot](screenshot2.png)
<br><br><br>

