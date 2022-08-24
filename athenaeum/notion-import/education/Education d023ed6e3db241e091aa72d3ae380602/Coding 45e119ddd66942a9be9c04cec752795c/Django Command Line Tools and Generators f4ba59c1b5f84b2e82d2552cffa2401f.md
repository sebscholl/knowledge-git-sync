# Django Command Line Tools and Generators

Last Edited: December 19, 2019 11:43 PM

Create new Django project:

$ django-admin startproject mysite

Run development server command:

$ python manage.py runserver

Generate new app directory:

$ python manage.py startapp APPNAME

To run Database Migrations:

$ python manage.py migrate

Generate model specific migrations:

$ python manage.py makemigrations APPNAME

Display SQL that will be executed when running migration):

$ python manage.py sqlmigrate APPNAME MIGRATION_NUMBER

Open Python shell for Django project:

$ python manage.py shell

Creating an admin user:

$ python manage.py createsuperuser

Run tests:

$ python manage.py test

Run tests by application:

$ python manage.py test APPNAME

Create superuser for project:

$ python manage.py createsuperuser —username=NAME —email=EMAIL

Change user password from CLI:

$ python manage.py changepassword *username*

Cache in database - run to configure database cache table:

$ python manage.py createcachetable