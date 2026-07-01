# Python Anywhere SETUP
YOU MUST CREATE AN ACCOUNT IN `pythonanywhere.com` for free site hosting

**Make your projects settings.py file ready for deployment**

```python
DEBUG = False

ALLOWED_HOSTS = ['mrshakil015.pythonanywhere.com']
or, ALLOWED_HOSTS = ['*']

import os
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

**Open bash console in pythonanywhere & delete all existing files**

```bash
rm -rf ~/*
rm -rf ~/.??*
```

**If you face permission denied error, give permission**

```bash
chmod -R 755 ~/folder_to_give_permission
```

**Upload your projects zip file & then unzip it**

```bash
unrar x filename.rar
```
or,
```bash
unzip filename.zip
```

**OR, you can also clone your project from github**

```bash
git clone your_repo_url
cd your_project_folder
```

**Create a WEB app with Manual Configuration**

- Set up source code `settings.py` location
- Set up WSGI Configuration path `manage.py` location
- Set up WSGI Configuration `DJANGO_SETTINGS_MODULE` to `folder_name.settings`
- Force https enabaled
- Reload your pages

**Apply migrations to create database**

```bash
python manage.py makemigrations app_name
python manage.py migrate
```
