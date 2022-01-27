# The Django Docs Tutorial 
To build a test site directly from the docs provided by Django.

## The work so far
I've completed through Part 3 so far.  After a brief detour through trying to get this up on Heroku, I will resume with [Part 4](https://docs.djangoproject.com/en/4.0/intro/tutorial04/).

This site is up and running at https://floating-taiga-14673.herokuapp.com/

## Heroku
In the venv set up for the project:
```
pip install django-heroku
pip install gunicorn
```
Update requirements.txt
```
del requirements.txt
pip freeze >> requirements.txt
```
Logged in to Heroku
```
heroku login
```
Create an App in Heroku
```
heroku create
```
>This failed with the warning
>
>`...You're using the staticfiles app without having set the STATIC_ROOT setting to a filesystem path.`

Looked in the settings file of my heroku getting started project and copied the following lines into mine at the bottom

Added at the top of the file
```
import django_heroku
import os
```
Added at the bottom of the file
```
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
STATIC_URL = "/static/"

# Configure Django App for Heroku.


django_heroku.settings(locals())
```
This workes to push it to heroku, but the file is still not running.

Looking at a solution from [stackoverflow](https://stackoverflow.com/questions/62599186/error-while-running-python-manage-py-collectstatic-noinput-even-though-i "Error while running '$ python manage.py collectstatic --noinput even though I have my static_root set") which mentions the following changes to settings.py:
```
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
STATIC_URL = '/static/'
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```
Copied over runtime.txt

Included requests in requirements

# [Part 4: Forms and generic views](https://docs.djangoproject.com/en/4.0/intro/tutorial04/)

We wrote a small form to vote on responses.

Then, we changed index, detail, and results to use generic views.