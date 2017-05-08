---
layout: post
title: "Load Flask into a Python Virtual Environment"
date: 2017-05-08
---
Following this tutorial [here](https://scotch.io/tutorials/build-a-crud-web-app-with-python-and-flask-part-one) by Mbithe Nzomo, here's the commands to quickly install virtualenv, virtualenvwrapper and then install Flask and it's dependancies into a virtualenv.

```
$ pip install virtualenv
$ pip install virtualenvwrapper
$ source /usr/local/bin/virtualenvwrapper.sh
```

Those three commands will get the basics installed, and then create a Python virtual environment with the following:

```
$ mkvirtualenv my-venv
$ workon my-venv
```

Now install Flask, simple:

```
$ pip install Flask
Collecting Flask
  Using cached Flask-0.12.1-py2.py3-none-any.whl
Collecting itsdangerous>=0.21 (from Flask)
Collecting click>=2.0 (from Flask)
  Using cached click-6.7-py2.py3-none-any.whl
Collecting Jinja2>=2.4 (from Flask)
  Using cached Jinja2-2.9.6-py2.py3-none-any.whl
Collecting Werkzeug>=0.7 (from Flask)
  Using cached Werkzeug-0.12.1-py2.py3-none-any.whl
Collecting MarkupSafe>=0.23 (from Jinja2>=2.4->Flask)
Installing collected packages: itsdangerous, click, MarkupSafe, Jinja2, Werkzeug, Flask
Successfully installed Flask-0.12.1 Jinja2-2.9.6 MarkupSafe-1.0 Werkzeug-0.12.1 click-6.7 itsdangerous-0.24
```

Running `pip freeze` will confirm it is installed, and list the dependancies that pip also installed:
```
$ pip freeze
appdirs==1.4.3
click==6.7
Flask==0.12.1
itsdangerous==0.24
Jinja2==2.9.6
MarkupSafe==1.0
packaging==16.8
pyparsing==2.2.0
six==1.10.0
Werkzeug==0.12.1
 ```
