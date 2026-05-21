# Email Sending Using Django

## Email Setting Configuration

### **1. Gmail SMTP Settings (Django)**

 **Important for Gmail**

To use Gmail with Django you must:

1. Enable **2-Step Verification**
2. Create an **App Password**
    - Go to: Google Account → Security → Search "App Passwords"
3. Use the generated 16-character password as `EMAIL_HOST_PASSWORD`.

**settings.py**

```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True

# Gmail requires an App Password (NOT your Gmail login password)
EMAIL_HOST_USER = 'your_email@gmail.com'
EMAIL_HOST_PASSWORD = 'your_app_password'

DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
```

### **2. Server / cPanel / Custom SMTP Settings**

**settings.py**

```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'mail.yourdomain.com'
EMAIL_PORT = 465
EMAIL_USE_SSL = True

EMAIL_HOST_USER = 'info@yourdomain.com'
EMAIL_HOST_PASSWORD = 'your_email_password'

DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
```

## **1. Using `send_mail` (Simple Email Sending)**

**views.py**

```python
from django.core.mail import send_mail

subject = "Test Email - Django send_mail"
message = "This is a plain text test email sent using send_mail."
from_email = "your_email@domain.com"
recipient_list = ["recipient@example.com"]

send_mail(
    subject,
    message,
    from_email, 
    recipient_list,
    fail_silently=False,
)
```

## 2**. Send mail Using `EmailMultiAlternatives` (HTML Email + Attachments)**

**views.py**

```python
from django.core.mail import EmailMultiAlternatives
from django.conf import settings
from django.template.loader import render_to_string

subject= "Welcome to EduDen"
recipient_email= email
sender_email=settings.EMAIL_HOST_USER
context = {
    'username':username,
    'email': email,
    'password': password
}
html_content= render_to_string("emails/confirm-mail.html", context)

email_send= EmailMultiAlternatives(subject, "" , sender_email, [recipient_email])
email_send.attach_alternative(html_content, "text/html")
email_send.send()    

```