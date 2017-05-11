---
layout: post
title: "Don't just copy and paste code tutorials, you'll learn nothing!"
date: 2017-05-11
---
I'm still going through this tutorial [here](https://scotch.io/tutorials/build-a-crud-web-app-with-python-and-flask-part-one) by Mbithe Nzomo, it's going well and I'm learning some interesting stuff on the way.

But I noticed that there really is a massive amount of code in this tutorial, lots of big Python & HTML files, and it's very tempting to just copy and paste from the tutorial straight into a file in the project. But doing so doesn't really teach you anything.

I have taken the approach to write out each file by hand, this helps in getting the reason behind the code into your head. As I am typing out each method or class I am thinking about what part the line of code plays in the finished app, and often when I try and run the end result in Flask locally I get an error which forces me to look back and find the erroneous syntax that is causing the error. It is a good way to learn how to debug code. If I copied and pasted each file into the repo and hit run, the tutorial would be over in a couple of hours. So far I have spent several evenings on it, and I'm learning more as a result.

Take the following for instance, I could have copied and pasted the whole of this code chunk from the tutorial into the relevant file in my [repo](https://github.com/molo76/project_dream_team), but would I have actually learned anything by doing so? By typing it all out by hand I feel I am actually learning the code and making the whole process of following the tutorial worthwhile.

In any case, this post is a good way to test out the markdown that adds syntax highlighting to code..p p p python! ;-)

```python
# app/auth/views.py

from flask import flash, redirect, render_template, url_for
from flask_login import login_required, login_user, logout_user

from . import auth
from forms import LoginForm, RegistrationForm
from .. import db
from .. models import Employee

@auth.route('/register', methods=['GET', 'POST'])
def register():
    """
    Handle requests to the /register route
    Add an employee to the db through the registration forms
    """
    form = RegistrationForm()
    if form.validate_on_submit():
        employee = Employee(email=form.email.data,
                            username=form.username.data,
                            fist_name=form.first_name.data,
                            last_name=form.last_name.data,
                            password=form.password.data)

        # add employee to the database
        db.session.add(employee)
        db.session.commit()
        flash('You have successfully registered! You may now login.')

        # redirect to the login page
        return redirect(url_for('auth_login'))

    # load registration template
    return render_template('auth/register.html', form=form, title='Resigster')

@auth.route('/login', methods=['GET', 'POST'])
def login():
    """
    Handle requests to the /login route
    Log an employee in through the login form
    """
    form = LoginForm()
    if form.validate_on_submit():

        # check whether employee exists in the database and whether
        # the password entered matches the password in the database
        employee = Employee.query.filter_by(email=form.email.data).first()
        if employee is not None and employee.verify_password(
                form.password.data):
            # log employee in
            login_user(employee)

            # redirect to the dashboard page after login_user
            return redirect(url_for('home.dashboard'))

        # when login details are incorrect
        else:
            flash('Invalid email or password.')

    # load login template
    return render_template('auth/login.html', form=form, title='Login')


@auth.route('/logout')
@login_required
def logout():
    """
    Handle requests to the /logout route
    Log an employee out through the logout link
    """
    logout_user()
    flash('You have successfully logged out.')

    # redirect to the login page
    return redirect(url_for('auth.login'))
```

I think that looks pretty good. I haven't taken to writing out the html files in the tutorial by hand, since I already know basic html, and I want to focus and crack on with the Python stuff. 
