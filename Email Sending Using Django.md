# Email Sending Using Django

There are only two options for email sending `send_mail()` and `EmailMultiAlternatives()`.

### Difference

| Method                   | Best For               |
| ------------------------ | ---------------------- |
| `send_mail()`            | simple emails          |
| `EmailMultiAlternatives` | advanced/custom emails |

**When `EmailMultiAlternatives` Is Better**

Use it if you need:

* attachments
* multiple content types
* embedded images
* advanced email handling

For normal HTML emails, `send_mail()` is perfectly fine.

### Gmail SMTP Settings

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

### Server / cPanel / Custom SMTP Settings

**Important for cPanel**

* Email Accounts
* Connect Devices
* Configure Mail Client

Go to:

```text id="jlwm3p"
Email Deliverability
```

Make sure:

* SPF enabled ✅
* DKIM enabled ✅

This is VERY important for Gmail inbox delivery.

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

# Common Ports

| Port | Security          |
| ---- | ----------------- |
| 587  | TLS (recommended) |
| 465  | SSL               |
| 25   | Unsecured/legacy  |

Usually:

* `587 + TLS` ✅ (upgraded version of SSL)
* or `465 + SSL`

## Using `send_mail()` (Simple Email Sending)

**views.py**

```python
from django.core.mail import send_mail

subject = "Test Email - Django send_mail"
text_message = "This is the plain text version. (Optional - it can be empty string)"
from_email = "your_email@domain.com"
to_email = ["recipient@example.com"]

send_mail(
    subject,
    text_message,
    from_email, 
    to_email,
    fail_silently=False,
    html_message=None, # You can use html string or template here
)
```

## Using `EmailMultiAlternatives()` (HTML Email + Attachments)

**views.py**

```python
from django.core.mail import EmailMultiAlternatives
from django.conf import settings
from django.template.loader import render_to_string

subject = "Welcome to EduDen"
text_content = "This is the plain text version. (Optional - it can be empty string)"
from_email = settings.EMAIL_HOST_USER
to_email = [email]

html_content= render_to_string(
    "emails/confirm-mail.html", 
    {
        'username':username,
        'email': email,
        'password': password
    }
)
email_send = EmailMultiAlternatives(
    subject, 
    text_content , # An alternative text if the html content fails to render.
    from_email, 
    to_email
)
email_send.attach_alternative(html_content, "text/html")
email_send.send()    

```

# Why Use Plain Text Too?

Best practice:

```python
text_content = "Welcome to our website."
```

Some email clients:

* block HTML
* prefer plain text
* use plain text as an alternative


# Email Template Styling Tips

Most email clients:

* do NOT support modern CSS fully
* ignore flex/grid sometimes

Use:

* inline CSS
* simple tables/divs
* minimal layouts

```html
<div style="font-family: Arial; padding: 20px;">

    <h2 style="color: #333;">
        Welcome
    </h2>

    <p>
        Thanks for joining.
    </p>

</div>
```

# Why your emails are being recognized as spam?

Gmail usually marks custom-domain emails as spam because your domain is missing proper email authentication records.

This is extremely common with new cPanel domains.

**Most Likely Fix for You**

Do these first:

1. Enable SPF + DKIM in cPanel
2. Add DMARC
3. Use `mail.pybrothers.top`
4. Wait some time for domain reputation
5. Avoid spammy email formatting

Those usually solve 80–90% of spam issues on cPanel hosting.