# Docker + Django + Nginx + uWSGI + Postgres

## 主要参考:
- https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-tutorial
- https://uwsgi-docs.readthedocs.io/en/latest/tutorials/Django_and_nginx.html

- [Django REST framework](http://www.django-rest-framework.org/)
- [利用 Django REST framework 编写 RESTful API](https://www.cnblogs.com/bayueman/p/6647641.html)
- [Vue+Django REST framework打造生鲜电商项目](https://blog.csdn.net/jamin2018/article/details/78907997)

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
(.venv) > $ pip install django djangorestframework psycopg2-binary uwsgi
```
### 创建项目
```
(.venv) > $ mkdir api
(.venv) > $ cd api
(.venv) > $ django-admin startproject django_rest_framework .
```



### 配置数据库
开发环境中，采用本地开发，并使用 Docker 搭建的 Postgres 数据库，具体的搭建过程可以参考 [docker-databases-with-adminer](https://github.com/keer2345/docker-databases-with-adminer) 。

#### 测试 Postgres 链接
```
(.venv) > ipython
In [1]: import psycopg2
In [2]: con = psycopg2.connect("host=127.0.0.1 port=54321 dbname=pgDB user=root password=123456")

```

#### Django 中的配置

`api/django_rest_framework/settings.py` :
```
DATABASES = {
    'default': {
        # SQLITE3
        #  'ENGINE': 'django.db.backends.sqlite3',
        #  'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),

        # POSTGRES
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'pgDB',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': 'localhost',
        'PORT': 54321,
    }
}
```

#### 同步数据库
```
python manage.py makemigrations
python manage.py migrate
```
#### 添加管理员
```
(.venv) > $ python manage.py createsuperuser
```

#### 运行项目
```
(.venv) > $ python manage.py runserver 0:8000
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

添加应用到配置文件中：
```python
INSTALLED_APPS = [
    # ...
    'rest_framework',
    'musics',
]

```
