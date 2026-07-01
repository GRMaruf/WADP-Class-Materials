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
