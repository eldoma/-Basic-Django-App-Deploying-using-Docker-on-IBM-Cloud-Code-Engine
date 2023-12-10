# Basic-Django-App-Deploying-using-Docker-on-IBM-Cloud-Code-Engine
Basic Django App Deploying using Docker, creating a Docker image, containerize &amp; share it on IBM Cloud Code Engine 

## Install these must-have packages and setup the Django environment.
- pip install --upgrade distro-info
- pip3 install --upgrade pip==23.2.1
- pip install virtualenv
- virtualenv djangoenv
- source djangoenv/bin/activate

### Install Django packages
- pip install Django

## Create Project
Create the First Django Project
- django-admin startproject firstproject

## Go to the Specific Project folder
- cd firstproject

### Create a Django app called firstapp within the project
- python3 manage.py startapp firstapp

## Make Migrations
Perform migrations to create necessary database tables
- python3 manage.py makemigrations

### Run Migration
- python3 manage.py migrate

### Start a development server hosting apps in the Specific Project Folder
python3 manage.py runserver

## After editing Views, App definitions, View Routes, paths
### Run Django Server in the project folder:

cd ..
python3 manage.py runserver

## Django will map any HTTP requests starting with /firstapp to firstapp and search any matches for paths defined in firstapp/urls.py.

### That's it, you should see your the HTTPResponse returned by your first view, which is a simple HTML page with content This is your first view.

after fixing another view (Date View)
- click on the launch application button to open the /date route you just created above 

# Containerizing the app using Docker

open the setting.py file and change the ALLOWED_HOSTS = [] code to:
- ALLOWED_HOSTS = ['*','.us-south.codeengine.appdomain.cloud']

install pipreqs
- pip install pipreqs
- pipreqs .

Run the following command to create an empty Dockerfile
- touch Dockerfile

Then open the newly created Dockerfile and copy the following contents to it.
# syntax=docker/dockerfile:1
FROM python:3
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

### run the following command to create and run the container image
- docker build . -t my-django-app:latest && docker run -e PYTHONUNBUFFERED=1 -p  8000:8000 my-django-app 

### launch the application
Click on Code Engine CLI Button

