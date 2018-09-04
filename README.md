# Docker + Django + Nginx + uWSGI + Postgres

## 主要参考:
- https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-tutorial
- https://uwsgi-docs.readthedocs.io/en/latest/tutorials/Django_and_nginx.html

## Nginx
- nginx/Dockerfile
- nginx/nginx.conf
- nginx/my_nginx.conf

## Django
### 搭建Django环境
```
virtualenv .venv
source .venv/bin/activate
```

```
(.venv) > $ pip install django djangorestframework psycopg2 uwsgi
```
### 创建项目
```
(.venv) > $ mkdir api
(.venv) > $ cd api
(.venv) > $ django-admin startproject django_rest_framework .
```
### 创建模型
```
(.venv) > $ python manage.py startapp musics
```

```
(.venv) > $ tree
.
├── django_rest_framework
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-36.pyc
│   │   └── settings.cpython-36.pyc
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── musics
    ├── admin.py
    ├── apps.py
    ├── __init__.py
    ├── migrations
    │   └── __init__.py
    ├── models.py
    ├── tests.py
    └── views.py
```
