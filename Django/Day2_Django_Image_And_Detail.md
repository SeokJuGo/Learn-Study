# ๐ DJANGO DAY 2 ๊ณต๋ถ

### ๐ง  1. REMIND

```python
$ conda activate django
# ์ฌ์ ์์ ํ์ผ๋ ๊ฐ์ํ๊ฒฝ์ ํ์ฑํํ์
$ python manage.py runserver
# ๊ธฐ์ต์ด ์๋๋ ์๋ฒ์ ๋ค์ ์ ์ํด๋ณด๊ธฐ 
```

## ๐ผ๏ธ 2. ์ด๋ฏธ์ง ์ถ๊ฐํด๋ณด๊ธฐ

```python
{% load static %}
<img src="{% static 'blog/jjanggu.png' %}" class="card-img-top" alt="...">
# ์ด๋ฏธ์ง ํ์ผ์ ๋ฏธ๋ฆฌ ์ค๋นํ์ฌ ์ ๊ณตํ๋ ๋ฐ ์ฌ์ฉํ๋ค.! 
```

### ๐ป 3. ๋ชจ๋ธ์ ์๋ก๋ ์ด๋ฏธ์ง๋ณ์&DB ์์ฑํด๋ณด๊ธฐ

```python
header_img = models.ImageField(upload_to='blog/images/%Y/%m/%d/', blank=True)
file_upload = models.FileField(upload_to='blog/files/%Y/%m/%d/', blank=True)
# ๊ด์ฉ์ ํ์ผ ๊ด๋ฆฌ๋ค /%Y/%m/%d/ # ๋/์/์ผ์ ์ฌ์ฉํ๋ค!
# ์ฅ๊ณ ์ ํน์ง์ธ ORM => DB์ถฉ๋์ด ์๊ธธ ์ ์๋ค.
```

### โ ๏ธ์ฃผ์โ ๏ธ Media File(์ฌ์ฉ์ ์๋ก๋ ํ์ผ)

```python
# backend/setting.py

from pathlib import Path
import os

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, '_media') 

```

```python
# board/models.py
head_image = models.ImageField(upload_to='board/images/%Y/%m/%d/', blank=True)

```

```python
# django_project/urls.py์ ์ถ๊ฐ

# ์ด๋ฏธ์ง ์๋ก๋ ํ๋๋ฅผ ์ํ ์ถ๊ฐ
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

#####

###### (์ด๋ฐ์์ผ๋ก ๊ธฐ์๋จ! #m) upload ํ์ผ๋ค์ ๊ผญ ๊ธฐ์ํด์ฃผ์!! #

### ๐ช 4. pk๋ง๋ค ๋ค๋ฅธ PostDetail ๋ค์ด๊ฐ๊ธฐ!

```python
# blog/views.py
class PostDetail(DetailView):
    model = Post
# ์ค๋ค์ดํฌํ์ผ๋ก post_detail์ ์ฌ์ฉํ  ์๋ ์๊ณ  post๋ฅผ ์ฌ์ฉํด๋ ๋๋ค!
```

```html
<!   post_detail  >
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    POST DETAIL
    {{ post.title }}
    {{ post.content }}
    {{ post.created_at }}
<!-- ์์ ์์ ํ๋ ๊ฑฐ์ฒ post์ ์ค๋ค์ดํฌํ post_detail ๋ ๋ค ๋๋ค  -->
</body>
</html>
```

```python 

# blog/urls.ppy
urlpatterns =+ path('<int:pk>/',views.PostDetail.as_view())
# '<int:pk>/' ํ์ฌ ์ฃผ์์์ pk ๋ฒํธ๋ก ๋ค์ด๊ฐ๋ฉด ๊ทธ์ ์์ํ๋ postDetail์ ๋ค์ด๊ฐ์ค๋ค!
```

![aaa](https://user-images.githubusercontent.com/116260619/218657895-c377c3d3-c50d-4a48-a54a-c5c7fc08f460.gif)
