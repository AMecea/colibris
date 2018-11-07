
## Starting Your Project

Go to your projects folder:

    cd ${PROJECTS_DIR}

Create a virtual environment for your new project:

    virtualenv .venv && source .venv/bin/activate

Install colibri:

    pip install git+https://gitlab.com/safefleet/colibri.git

Prepare the project:

    colibri-start-project <project-name> --template git@gitlab.com:safefleet/microservice-template.git 

Your project folder will contain a package derived from your project name as well as various other stuff.

The rest of the steps assume you're in your project folder and you have your virtual environment correctly sourced.


## Database

Set your database URL by editing the `settings.py` file:

    nano settings.py 


## Models

Add your models by editing the `models.py` file:

    nano ${PACKAGE}/models.py 


## Schemas

Add your schemas by editing the `schemas.py` file:

    nano ${PACKAGE}/schemas.py 


## Views

Add your views by editing the `views.py` file:

    nano ${PACKAGE}/views.py


## Routes

Associate URL paths to views by editing the `routes.py` file: 

    nano ${PACKAGE}/routes.py


## Authentication & Authorization

Choose a backend for both the authentication and authorization mechanisms by setting the corresponding variables
in the `settings.py` file:

    nano ${PACKAGE}/settings.py


## Web Server

Start the web server by running:

    ./manage.py runserver

Then you can test it by pointing your browser to:

    http://localhost:8888


## Migrations

#### Create Migrations

To create migrations for your model changes, use:

    ./manage.py makemigrations

You can optionally specify a name for your migrations:

    ./manage.py makemigrations somename

#### Apply Migrations

To apply migrations on the currently configured database, use:

    ./manage.py migrate


## Settings

Here's a list of available settings and their default values:

#### `PROJECT_PACKAGE_NAME`

Sets the main project package name. Defaults to `'<projectname>'`.

#### `DEBUG`

Enables or disables debugging. Defaults to `True`.

#### `LISTEN`

Controls the interface(s) on which the server listens. Defaults to `'0.0.0.0'`.

#### `PORT`

Controls the server TCP listening port. Defaults to `8888`.

#### `MIDDLEWARE`

A list of all the middleware functions to be applied, in order, to each request/response. Defaults to:

    [
        'colibri.middleware.handle_errors_json',
        'colibri.middleware.handle_auth',
    ]

#### `AUTHENTICATION`

Configures the authentication backend. Should be defined as a dictionary with at least one entry, `backend`,
representing the python path to the backend class. The rest of the entries are passed as arguments to the constructor.

Defaults to `None`, which effectively disables authentication.

#### `AUTHORIZATION`

Configures the authorization backend. Should be defined as a dictionary with at least one entry, `backend`,
representing the python path to the backend class. The rest of the entries are passed as arguments to the constructor.

Defaults to `None`, which effectively disables authorization, allowing access to all resources for any authenticated
request.

#### `DATABASE`

Sets the project database.
See [this](http://docs.peewee-orm.com/en/latest/peewee/database.html#connecting-using-a-database-url) for examples of
database URLs.

Defaults to `'sqlite:///<projectname>.db'`

#### `LOGGING`

Configures the logging mechanism.
See [logging.config](https://docs.python.org/3.7/library/logging.config.html) for details.