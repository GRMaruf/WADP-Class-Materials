# Django Basic FBV Authentication

## 1. Create Models
Create a custom model for authentication.

``` python
from django.contrib.auth.models import AbstractUser

class UserModel(AbstractUser):
    USER_TYPE = {
        ('Teacher', 'Teacher'),
        ('Student', 'Student'),
    }
    user_type = models.CharField(max_length=20)
    def __str__(self):
        return self.name
```

## 2. Configure Settings
In `settings.py` file:

``` python
INSTALLED_APPS = [
    ...
    'app_name',
    ...
]

AUTH_USER_MODEL = 'app_name.UserModel'
LOGIN_URL = 'login'
```

## 3. Run Commands
In terminal:

``` bash
py manage.py makemigrations
py manage.py migrate
```

## 4. Write View Functions
In `views.py` file:

``` python
from django.shortcuts import render, redirect
from .models import UserModel
from django.contrib.auth import authenticate, login, logout
from django.contrib.auth.decorators import login_required
from django.http import HttpResponse

def register_view(request):

    if request.method == 'POST':
        username = request.POST['username']
        user_type = request.POST['user_type']
        password = request.POST['password']
        confirm_password = request.POST['confirm_password']

        if password == confirm_password:
            user = UserModel.objects.create_user(
                username=username,
                user_type=user_type,
                password=password
            )
            if user:
                return redirect('login')
    
    return render(request, "register.html")

def login_view(request):

    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']

        user = authenticate(request, username=username, password=password)
        if user:
            login(request, user)
            return redirect('dashboard')
        
    return render(request, "login.html")

@login_required
def logout_view(request):
    logout(request)
    return HttpResponse("You have logged out successfully.")

@login_required
def dashboard(request):
return render(request, 'dashboard.html')
```

## 5. Set URLs
In app's `urls.py` file:

``` python
from django.urls import path
from .views import *

urlpatterns = [
    path('register/', register_view, name='register'),
    path('login/', login_view, name='login'),
    path('logout/', logout_view, name='logout'),
    path('dashboard/', dashboard, name='dashboard'),
]
```

In project's `urls.py` file:

``` python
from django.urls import path, include

urlpatterns = [
    ...
    path('', include('app_name.urls')),
]
```

## 6. Create Templates
Inside your app create a `templates` folder, add a `base.html` file.

``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous" />
    <title>Simple FBV Auth</title>
  </head>
  <body>
    {% block body %}

    {% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
  </body>
</html>
```

Add a `register.html` file.

``` html
{% extends 'base.html' %}

{% block body %}
<h1 class="text-center mt-5">Register User</h1>

<form method="post" class="card m-3 p-3 w-50 mx-auto">
    {% csrf_token %}
    <label>Username:</label>
    <input type="text" name="username" class="form-control mb-3">
    <label>User Type:</label>
    <select name="user_type" class="form-select mb-3" required>
        <option selected disabled>Select User Type</option>
        <option value="Teacher">Teacher</option>
        <option value="Student">Student</option>
    </select>
    <label>Password:</label>
    <input type="password" name="password" class="form-control mb-3">
    <label>Confirm Password:</label>
    <input type="password" name="confirm_password" class="form-control mb-3">

    <button class="btn btn-primary" type="submit">Submit</button>
</form>
{% endblock %}
```

Add a `login.html` file.

``` html
{% extends 'base.html' %}

{% block body %}
<h1 class="text-center mt-5">Login User</h1>

<form method="post" class="card m-3 p-3 w-50 mx-auto">
    {% csrf_token %}
    <label>Username:</label>
    <input type="text" name="username" class="form-control mb-3">
    <label>Password:</label>
    <input type="password" name="password" class="form-control mb-3">

    <button class="btn btn-primary" type="submit">Submit</button>
</form>
{% endblock %}
```

Add a `dashboard.html` file:

``` html
{% extends 'base.html' %}

{% block body %}
  <h1 class="text-center mt-5">Dashbord</h1>

  <div class="text-center mt-5">
    <a href="{% url 'logout' %}" class="btn btn-primary p-5 fw-bold">Logout From Dashbord</a>
  </div>
{% endblock %}
```

## 7. Now Run Development Server
In the terminal:
``` bash
py manage.py runserver
```