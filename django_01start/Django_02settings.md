# settings.py
```
#coding:utf-8

import os

BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

SECRET_KEY = '-*%&p9zku$*fy-a6uxw##%40d&ze@l+sr)_yk!f0^4fqxvyh-6'

DEBUG = True

ALLOWED_HOSTS = []

INSTALLED_APPS = [ #应用信息
    'django.contrib.admin', #自带的admin站点
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',#你创建的app
]

MIDDLEWARE = [ #中间件信息
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    # 'django.middleware.csrf.CsrfViewMiddleware', #csrf表单安全验证，form可以跨域post数据，先注释
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
#CSRF（Cross Site Request Forgery），跨站点请求伪造

ROOT_URLCONF = 'mysite.urls' #根路由位置

TEMPLATES = [ #模板相关信息
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # 'DIRS': [], 
        #这是原配置文件信息，没有默认加上，如果是pycharm创建django会有，其他默认配置也会加上
        'DIRS': [os.path.join(BASE_DIR, 'templates')], #这行必须有，要不然会报TemplateDoesNotExist错误
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'mysite.wsgi.application'

DATABASES = { #数据库相关信息
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    # },
    'default':{
        'ENGINE':'django.db.backends.mysql',
        'NAME':'myappdb', #你的数据库名称
        'USER':'root',#数据库用户名
        'PASSWORD':'123456', #密码
        'HOST':'', #数据库所在的主机，留空默认为localhost
        'PORT':3306,
    }
    '''
执行python manage.py makemigrations可能会报错说：加载MySQLdb模块错误，因为Django默认的驱动就是MySQLdb，
由于python3对pymysql支持有好，所以我们用pymysql。修改Django应用配置setting.py所在的那个文件夹中的
__init__.py文件，加入以下内容：
import pymysql
pymysql.install_as_MySQLdb()
    '''
}

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

# LANGUAGE_CODE = 'en-us' #默认语言
LANGUAGE_CODE = 'zh-hans' #中文

TIME_ZONE = 'UTC' #默认时区

USE_I18N = True

USE_L10N = True

USE_TZ = True



STATIC_URL = '/static/' 
#默认别名，前端引入的时候用的都是这个，无论下面的static变成什么名称

STATICFILES_DIRS = ( #必须加上，要不然静态文件就not found 了
        os.path.join(BASE_DIR, 'myapp', 'static'),
    )
"""
这个是真实的静态文件绝对路径，如果每个应用的静态文件夹放在各自的应用下面则，要加上应用(文件夹)名称。
其他应用也可以访问到这个路径下面的静态文件，如果路径和文件一致的话。
"""

# 日志文件配置
# 下面这些配置可以看到数据库操作的原生语句
# LOGGING = {
#     'version': 1,
#     'disable_existing_loggers': False,
#     'handlers': {
#         'console':{
#             'level':'DEBUG',
#             'class':'logging.StreamHandler',
#         },
#     },
#     'loggers': {
#         'django.db.backends': {
#             'handlers': ['console'],
#             'propagate': True,
#             'level':'DEBUG',
#         },
#     }
# }





```