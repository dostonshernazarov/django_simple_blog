# django_simple_blog

# 1. Loyiha sozlamalari
 **manage.py**
  * Loyihangizni boshqarish uchun buyruq qatori vositasi. Server ishga tushirish, migratsiyalar bajarish va super foydalanuvchilar yaratish kabi vazifalar uchun qo‘llaniladi.

 **blog_project/settings.py**
  * Loyiha uchun asosiy sozlash fayli. U o‘rnatilgan dasturlar, ma’lumotlar ombori, migratsiyalar, andozalar va boshqa sozlamalarni o‘z ichiga oladi.

#
# 2. Blog app yaratish
  ```bash
  python manage.py startapp blog
  ```
  ```startapp```: loyiha doirasida yangi ilova yaratadi. Ilovalar Django tizimining modulli tarkibiy qismlari hisoblanib, har bir ilova o‘ziga xos vazifalarni bajaradi.

## Yaratilgan filelar
 **blog/models.py**
  * Ilovaning ma’lumotlar tuzilmasini (ma’lumotlar bazasi sxemasini) belgilaydi.

 **blog/views.py**
  * So‘rovlarni qayta ishlash va javoblarni taqdim etish mantiqini o‘z ichiga oladi.

 **blog/admin.py**
  * Django‘ning o‘rnatilgan administrator interfeysi orqali ilovangizning ma’lumotlarini boshqarish imkoniyatini beradi.

 **blog/apps.py**
  * Ilovangiz uchun meta-axborot (masalan, ilova nomi).
#

# 3. Dastur sozlamalari
  ```python
  INSTALLED_APPS = [
    ...
    'blog',
  ]
  ```
  * Djangoga blog ilovasini loyihaga kiritishni ko‘rsatadi. Bunsiz, Django ilovangizni tanib olmaydi.

#
# 4. Blog modelini ishlab chiqish
  ```python
  from django.db import models  # Import Django's database models module.

class Post(models.Model):  # Define a model called Post.
    title = models.CharField(max_length=200)  # A string field for the blog title.
    content = models.TextField()  # A text field for the blog content.
    created_at = models.DateTimeField(auto_now_add=True)  # Automatically saves the timestamp when the post is created.

    def __str__(self):  # A string representation of the object.
        return self.title  # Returns the title of the post.
  ```

 **blog/models.py**
  * models.Model: Djangoda modellarni belgilash uchun asosiy sinf.
  * CharField: Sarlavhalar uchun mos keladigan qisqa matn maydoni. max_length parametri uning hajmini cheklaydi.
  * TextField: Blog tarkibini saqlash uchun katta matn maydoni.
  * DateTimeField: Sana va vaqtni saqlaydi. auto_now_add=True parametri post yaratilganda joriy vaqt belgilanishini avtomatik ravishda o‘rnatadi.
  * __str__ metodi: Bu obyektning satr sifatida qanday ko‘rsatilishini belgilaydi (masalan, admin panelida).

#
# 5. Migratsiyalar yaratish
  ```python
  python manage.py makemigrations
  python manage.py migrate
  ```
  * ```makemigratsiyalar```: ma’lumotlar bazasi jadvallarini yaratish yoki o‘zgartirish uchun zarur bo‘lgan SQL ko‘rsatmalarini tayyorlab beradi.
  * ```migrate```: SQL ko‘rsatmalarini bajarib, ma’lumotlar bazasiga o‘zgartirishlarni qo‘llaydi.

#
# 6. Modelni administratorga ro‘yxatdan o‘tkazish
 **blog/admin.py**
  ```python
  from django.contrib import admin  # Import the admin module.
from .models import Post  # Import the Post model.

admin.site.register(Post)  # Registers the Post model with the admin interface.
  ```
  * ```admin.site.register(Post)```: Administrator paneli orqali Post obyektlarini boshqarish imkoniyatini ta’minlaydi.

#
# 7. Ko‘rinishlar yaratish
 **blog/views.py**
  ```python
  from django.shortcuts import render  # Import the render function.
from .models import Post  # Import the Post model.

def post_list(request):  # Define a view called post_list.
    posts = Post.objects.all()  # Fetch all blog posts from the database.
    return render(request, 'blog/post_list.html', {'posts': posts})  # Render the template with the posts.
  ```
  * ```render```: Andozani kontekst ma’lumotlari bilan birlashtiradi va HTTP javobini qaytaradi.
  * ```Post.objects.all()```: Post jadvalidagi barcha yozuvlarni oladi.
  * ```{’posts’: posts}```: Andozaga uzatiladigan ma’lumotlarni o‘z ichiga olgan lug‘at.

#
# 8. URL manzillarni sozlash (Router)
 **blog/urls.py**
  ```python
  from django.urls import path  # Import the path function.
from . import views  # Import the views module.

urlpatterns = [  # Define a list of URL patterns.
    path('', views.post_list, name='post_list'),  # Map the root URL to the post_list view.
]
  ```

  **blog_project/urls.py**
   ```python
   from django.contrib import admin  # Import admin functionality.
from django.urls import path, include  # Import path and include.

urlpatterns = [
    path('admin/', admin.site.urls),  # Admin URL.
    path('', include('blog.urls')),  # Include URLs from the blog app.
]
  ```
  * ```include('blog.urls')```: Blog ilovasiga yo‘naltirishni o‘tkazadi.

#
# 9. HTML shablonlar yaratish
 **blog/templates/blog/post_list.html**
  ```html
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blog</title>
</head>
<body>
    <h1>Blog Posts</h1>
    {% for post in posts %}  <!-- Loop over posts passed from the view. -->
        <h2>{{ post.title }}</h2>  <!-- Display the post title. -->
        <p>{{ post.content }}</p>  <!-- Display the post content. -->
        <small>{{ post.created_at }}</small>  <!-- Display the creation date. -->
        <hr>
    {% endfor %}
</body>
</html>
  ```

 * ```{% for post in posts %}```: Ma’lumotlar ustida sikl bajarish uchun Django‘ning andoza tili.
 * ```{{ post.title }}```: Har bir postning sarlavhasini chiqaradi.

#
# 10. Dastur serverini ishga tushirish
  ```bash
  python manage.py runserver
  ```
  * Dastur ```http://127.0.0.1:8000``` manzilida ishga tushadi.

#
# 11. Administrator paneli orqali maqolalar qo‘shish
 * http://127.0.0.1:8000/admin manziliga super foydalanuvchi hisobi bilan kirib, bir nechta post yarating. Bu postlar bosh sahifada ko‘rinadi.