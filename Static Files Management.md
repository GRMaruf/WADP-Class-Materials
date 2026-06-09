# Static Files Management
Websites generally need to serve additional files such as images, JavaScript, or CSS. In Django, we refer to these files as “static files”. Django provides django.contrib.staticfiles to help you manage them.

## Static Files in DEBUG Mode

**In `setings.py` file:**
```python
STATIC_URL = 'static/'
STATICFILES_DIRS = [
    BASE_DIR / "myApp" / "static",
]
```

**In `static/css/mycss.css` file inside app's folder:**
```css
body {
    background-color: aqua;
}
h1 {
    color: blue;
}
```

**In `templates/home.html` file: inside app's folder**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="{% static 'css/mycss.css' %}">
    <title>Document</title>
</head>
<body>
    <h1>Home</h1>
</body>
</html>
```

## Extra Configuration for PRODUCTION Mode

**Install `whitenoise`:**
```bash
pip install whitenoise
```

**In `settings.py` file:**
```python
DEBUG = False
ALLOWED_HOSTS = ['*']

MIDDLEWARE = [
    # ...
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",
    # ...
]

STATIC_ROOT = BASE_DIR / "staticfiles"
STORAGES = {
    "staticfiles": {
        # This triggers web browsers to automatically pull newly deployed file modifications instead of fetching stale cached versions.
        "BACKEND": "whitenoise.storage.CompressedManifestStaticFilesStorage",
        # For without compression, use this backend "django.contrib.staticfiles.storage.ManifestStaticFilesStorage"
        # For Cloud Object Storage Engine (Amazon S3 / R2), use "storages.backends.s3boto3.S3Boto3Storage" which requires  "pip install django-storages[boto3]"
    },
}
```

**Collect Static All Files into `STATIC_ROOT`:**
```bash
python manage.py collectstatic
```
