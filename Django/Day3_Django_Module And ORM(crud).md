# โ๏ธ DJANGO DAY 3 ๊ณต๋ถ

### ๐ 1. REMIND

```python
$ conda activate django
# ์ฌ์ ์์ ํ์ผ๋ ๊ฐ์ํ๊ฒฝ์ ํ์ฑํํ์
$ python manage.py runserver
# ๊ธฐ์ต์ด ์๋๋ ์๋ฒ์ ๋ค์ ์ ์ํด๋ณด๊ธฐ 
```

## ๐คผ 2. ๋ชจ๋ํ

##### base.html์ ๋ง๋ค์ด ๊ณตํต ์์ญ๋ง ํ์ผ๋ก ๋จ๊ฒจ๋ 

```python
#blog/post_list.html
          {% extends 'board/base.html' %}
					
          {% block page_area %}
            <section class="py-5">
						  ... ์๋ต ...
            </section>
            {% endblock %}
```

### ๐ 3. ORM ์ ๊ทผํด์ CRUD ํด๋ณด๊ธฐ!

```python
# ํฐ๋ฏธ๋์์ shell ์ 
$ python manage.py shell  
```

```python
# shell์์ ํ์ธํด๋ณผ ๋ด์ฉ
from ์ฑ.models import ํด๋์ค๋ช 
>>> from blog.models import Post
```

### 1. Create

```python
p1 = Post() 
p2 = Post(title="Second", content="Django")
p2.save()
Post.objects.create(title="Third", content="django") # ์ ์ฅ ๋ฐ๋ก๋จ!
```

### 2. Read

```python
# Read
Post.objects.all() # ์ ๋ถ๋ค ๊ฐ์ ธ์ค๊ธฐ
# select * from blog_post where id=3;
Post.objects.filter(id=3)
Post.objects.get(id=3)

# SELECT * FROM blog_post WHERE title LIKE '%๊ธ%';
Post.objects.filter(title__contains='๊ธ') 
Post.objects.filter(title__icontains='๊ธ')

Post.objects.filter(title__contains='Third')  
Post.objects.filter(title__icontains='Third') # icontains ๋์๋ฌธ์ ๊ตฌ๋ถ์ํจ
Post.objects.filter(title__exact='Third')  # ๊ผญ ๊ทธ ๋ฌธ์์ด์ ๊ฒ์ํด์ฃผ๋ ๋ฉ์๋

Post.objects.filter(title__exact='Third').first() # ํ๋๋ง

Post.objects.filter(id__gt=3) # 3๊ฐ ์ด์
# in ํจ์
Post.objects.filter(id__in=[3, 6, 9])
Post.objects.filter(content__in=['Django', 'django', 'jango'])

# ํ๊ท , ์ต์, ์ต๋, ํฉ๊ณ
from django.db.models import Avg, Max, Min, Sum
Post.objects.all().aggregate(Avg('id')) #ํ๊ท 

Post.objects.all().count() #์ ์ฒด

```

### 3. Update

```python
p3 = Post.objects.get(id=4)
p3.title = '์ ๋ชฉ ๋ณ๊ฒฝ'
p3.save()
```

### 4. Delete

```python
# Delete
p3.delete()
Post.objects.filter(id__lte=4).delete()
```


