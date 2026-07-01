# Shared Hosting (C Panal) SETUP

In `settings.py`:
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

# Or, Configure STATICFILES_STORAGE with caching support
STORAGES = {
    # ...
    "staticfiles": {
        "BACKEND": "whitenoise.storage.CompressedManifestStaticFilesStorage",
    },
}
```


