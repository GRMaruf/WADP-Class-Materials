# Media Files Management

## Media Files in DEBUG Mode
**In `settings.py` file:**
```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

**In `urls.py` file inside project folder:**
```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... the rest of your URLconf goes here ...
]

# Serve media files during development
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

**Create your models with image or other media files:**
```python
class Image(models.Model):
    image = models.ImageField('Upload Image', upload_to='images', null=True)
```
If you are using `ImageField`, you must install `pillow`.
```bash
pip install pillow
```

**Image preview in `admin.py` file:**
```python
from django.utils.html import format_html
from .models import Image

class ImageAdmin(admin.ModelAdmin):
    # Create a custom field 'image_preview' to render the HTML img tag
    def image_preview(self, obj):
        if obj.image:
            return format_html('<img src="{}" style="max-width: 100px; max-height: 100px;" />', obj.image.url)
        return "No Image"
    
    image_preview.short_description = 'Preview'

    # Add 'image_preview' to your list display
    list_display = ['image_preview']

admin.site.register(Image, ImageAdmin)
```

**Show specific or all the images in template:**
```html
    <!--Without models-->
    <img src="/media/images/SEO.jpg" alt="Alter" width="200">

    <!--pass models-->
    {% for i in images %}
    <br>
    <img src="{{ i.image.url }}" alt="Alter" width="200">
    {{i.image.url}}
    {% endfor %}
```







