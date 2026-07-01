# Shared Hosting (C Panal) SETUP

**Install `whitenoise`**
```bash
pip install whitenoise
pip install whitenoise[brotli] # file compression is faster in brotli format

# Whitenoise Documentation: [whitenoise.readthedocs.io/](https://whitenoise.readthedocs.io/en/latest/)
```

**In `settings.py`**
```python
DEBUG = False

ALLOWED_HOST = ['*', 'your_domain_name.com'] # '*' is not recommended

INSTALLED_APPS = [
    ...
    'whitennoise.runserver_nostatic', # uses 'whitenoise' also in development, right before 'staticfiles'
    'django.contrib.staticfiles',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    "whitenoise.middleware.WhiteNoiseMiddleware", # right next to 'SecurityMiddleware'
    ...
]

STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'static'
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'

# Configure STATICFILES_STORAGE without caching support
STATICFILES_STORAGE = "whitenoise.storage.CompressedStaticFilesStorage"
# Or,
# Configure STATICFILES_STORAGE with caching support
STORAGES = {
    # ...
    "staticfiles": {
        "BACKEND": "whitenoise.storage.CompressedManifestStaticFilesStorage",
    },
}

# Faster File Serving with CDN
STATIC_HOST = "http://...cdn_link
STATIC_URL = STATIC_HOST + "/static/"

# In production, set the environment variable 'STATIC_HOST' from C Panal, then retrive it here
# STATIC_HOST = os.environ.get("DJANGO_STATIC_HOST", "")

# In Heroku, you can set environment variables like this:
# $ heroku config:set DJANGO_STATIC_HOST = http://...cdn_link
```

**In `urls.py`**
```python
from django.urls import re_path
from django.conf import settings
from django.conf.urls.static import static
from django.views.static import serve

# Must use a comma at the end, or, need to use append() function
urlpatterns+=re_path(r'^static/(?P<path>.*)$', serve, {'document_root': settings.STATIC_ROOT}), 
urlpatterns+=re_path(r'^media/(?P<path>.*)$', serve, {'document_root': settings.MEDIA_ROOT}),
```

**MySQL SETUP**
```bash
pip install mysqlclient
```
If there is any flags error, install like this:
```bash
MYSQLCLIENT_CFLAGS = "$(mysql_config --cflags)" \
MYSQLCLIENT_LDFLAGS = "$(mysql_config --libs)" \
pip install mysqlclient
```
Alternative for `mysql` similar but slower:
```bash
pip install pymysql
```
If you are using 'pymysql', you must import it from your project's `__init__.py` file:
```python
import pymysql
pymysql.install__as_MySQLdb()
```
*Creating your MySQL Database from cPanal*
 - In cPanal, go to 'Manage My Database' (by search)
 - Create a database named 'pybrothe_grmaruf_job_portal'
 - Create a user with username ('pybrothe_grmaruf') and password
 - Asign the user to this database providing all the privilages

In **settings.py** file
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql', # Fixed for mysql
        'NAME': 'pybrothe_grmaruf_job_portal', # Your database name
        'USER': 'pybrothe_grmaruf', # The user who is assigned to the database
        'PASSWORD': '564151.faoe', # User password
        'HOST': 'localhost', # Use your database domain (domain.com), if using other hosting site for database
        'PORT': '3306', # Fixed for mysql
    }
        # For Production use, it is recommended to use environment variables for 'NAME', 'USER', 'PASSWORD' and 'HOST'
}
```

**PostgreSQL SETUP**
```bash
pip install psycopg2
pip install psycopg2-binary # better for cPanal
```
*Check your cPanal's version, make sure that version supports your Django version, then install supported Django*
```bash
pip install "Django==4.2.23"
```
*Creating your PostgreSQL Database from cPanal*
 - In cPanal, go to 'PostgreSQL Database' (by search)
 - Create a database named 'pybrothe_grmaruf_job_portal'
 - Create a user with username ('pybrothe_grmaruf') and password
 - Asign the user to this database providing all the privilages

In **settings.py** file
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql', # Fixed for PostgreSQL
        'NAME': 'pybrothe_grmaruf_job_portal', # Your database name
        'USER': 'pybrothe_grmaruf', # The user who is assigned to the database
        'PASSWORD': '564151.faoe', # User password
        'HOST': 'localhost', # Use your database domain (domain.com), if using other hosting site for database
        'PORT': '5432', # Fixed for PostgreSQL
    }
        # For Production use, it is recommended to use environment variables for 'NAME', 'USER', 'PASSWORD' and 'HOST'
}
```

**Prepare `requirements.txt` file**
```bash
pip freeze > requirements.txt
```

**cPanal SETUP**
 1. Search for 'Domain', and create a subdomain, or you can the existing domain.
 2. Search for 'Setup Python App', select recommended python version, use default derectory ('home/') or use your own ('home/GRMaruf/testApp'), select the domain/subdomain you want to use, then press `Create` button.
 3. Search for 'FileManager', find your app directory, upload your project as zip and then unzip it.
 4. Edit `passanger_wsgi.py` file with this:
```python
from project_folder.wsgi import application # Use the folder where wsgi.py file exists
```
 5. Search for 'Setup Python App', copy the (virtual env) comm


**To Clean up Caches**
```bash
pip cache purge
```
