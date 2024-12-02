# Django blog loyihasi

Bu Django yordamida yaratilgan oddiy blog ilovasidir. Ilova foydalanuvchilarga sarlavhalar va mazmunli blog yozuvlarini ko‘rish imkonini beradi.

---

## Xususiyatlar

- Blog yozuvlari ro‘yxatini ko‘rsatish.
- Har bir yozuvda sarlavha, mazmun va yaratilgan vaqt belgisi mavjud.
- Django Model-View-Template (MVT) arxitekturasi asosida qurilgan.
- Loyihani oddiy va boshlovchilar uchun qulay o‘rnatish.

---

## Talablar

- Python 3.9+
- Django 4.0+
- Virtual muhit vositasi (ixtiyoriy, ammo tavsiya etiladi)

---

## O‘rnatish va sozlash

Loyihani mahalliy kompyuterda o‘rnatish va ishga tushirish uchun quyidagi bosqichlarni bajaring.

### 1. Repozitoriyni klonlash
```bash
  git clone https://github.com/yourusername/django-blog.git
  cd django-blog
```

## Virtual muhit yaratish
```bash
  python -m venv venv
  source venv/bin/activate  # For Linux/Mac
  venv\Scripts\activate     # For Windows
```

## Bog‘liqliklarni o‘rnatish
```bash
  pip install django
```

## Ma’lumotlar bazasi migratsiyalarini qo‘llash
```bash
python manage.py makemigrations
python manage.py migrate
```

## Loyiha serverini ishga tushiring
```bash
python manage.py runserver
```

## Ilovaga kirish
```bash
http://127.0.0.1:8000/
```


