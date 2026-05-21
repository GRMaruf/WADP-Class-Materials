# How to Set Favicons
In `base.html` file:

```html
{% load static %}
...
<link rel="icon" type="image/png" href="{% static 'images/favicon.png' %}">
<link rel="apple-touch-icon" href="{% static 'images/favicon.png' %}">
```