# Start Django
1、**关于Django版本你可能会用到以下命令**  
- 查看Django版本
```
python -m django --version    
```
- 安装指定版本的Django
```
pip install django==2.1(版本号:自己选)
```

2、**创建一个Django项目**
- 创建项目命令
```
django-admin startproject mysite(项目名称：自己定义)
```
- 执行上述命令之后会看到下面的文件夹目录结构
```
mysite/                       
    manage.py                   #管理django的
    mysite/                   
        __init__.py
        settings.py             #项目配置文件
        urls.py                 #配置路由的
        wsgi.py                 #WSGI 百度了解下
```

3、**开始创建web应用**  
- 在manage.py文件所在的目录，执行以下命令，创建应用

```
python manage.py startapp myapp(程序名称，自定义的)
```
- 会在这个文件夹中创建一个新的文件夹，目录结构如下：

```
myapp/
    migrations/             #和ORM相关
        __init__.py
    __init__.py
    admin.py                #在django自带的admin站点中注册模型或其他的配置
    apps.py                 #和
    models.py               #模型，数据库表，字段，数据类型等等的定义
    tests.py                #单元测试用的
    views.py                #视图，在urls中配置好路径后，前端访问的相当于视图中的函数
```

4、**写第一个视图(views.py)**  
- myapp/views.py文件里面编辑以下内容
```
from django.shortcuts import HttpResponse

def index(request):
    return HttpResponse('这是首页')#每个视图返回的必须是HttpResponse对象
```
- 在应用目录下创建一个urls.py文件来配置url,编辑 myapp/urls.py

```
from django.urls import path, re_path
from . import views

urlpatterns = [
    re_path(r'^$', views.index),#默认访问index页面
    path('index',views.index,name='index'),#和上边的访问返回结果一样
]
#path(路由(正则),视图函数,别名)
```
- 对根url进行配置，编辑mysite/urls.py

```
from django.contrib import admin
from django.urls import path, re_path, include

urlpatterns = [
    path('myapp/', include('myapp.urls'),namespace='myapp'),
    # 导入myapp.urls中的url配置，
    # namespace这边写了之后，在相应的应用的urls文件中要添加app_name='myapp'全局变量，这主要目的是防止应用间的路由串了
    path('admin/', admin.site.urls),#这个是默认的，留着访问管理员页面用的
]
```
5、**启动Django**
- 在manage.py文件所在的文件夹下，右击选择“在此处打开命令窗口”，输入以下命令
```
python manage.py runserver 8888(端口号可加可不加，默认为8000)
```

- 现在就可以去执行python manage.py runserver,启动成功之后，浏览器访问http://127.0.0.1:8000/myapp，路径后面也可以再加上/index,就会看到views.py里面index函数中的内容了。



