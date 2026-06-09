# Static Files Management
## Static Files in DEBUG Mode

**In `setings.py` file:**
```python
STATIC_URL = 'static/'
STATICFILES_DIRS = [
    BASE_DIR / "main" / "static",
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
```
</html>
# Static Files in PRODUCTION Mode
