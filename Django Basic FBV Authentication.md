# Django Basic FBV Authentication

# 1. Create Models

""" bash\
from django.contrib.auth.models import AbstractUser

class UserModel(AbstractUser):
    USER_TYPE = {
        ('Teacher', 'Teacher'),
        ('Student', 'Student'),
    }
    user_type = models.CharField(max_length=20)
    def __str__(self):
        return self.name
"""