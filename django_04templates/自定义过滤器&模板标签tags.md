# 自定义过滤器&模板标签tags
需要在应用下先创建一个 **templatetags** 库，里面写一些自定义的tags或者filter，文件命名方式：**自定义_tags.py**

目录结构：
```
templatetags/
    __init__.py
    my_tags.py
```

#### my_tags.py
```
from django import template
register = template.Library() #这行是固定不变的，必须有，而且对象名字只能是register

#自定义过滤器
@register.filter
def filter_multi(x, y): #过滤器只支持两个参数
	"""
	用法：{{ x|filter_multi:y }}
	"""
	return x*y
	
#自定义tag
@register.simple_tag
def tag_multi(x,y,z): #不限制参数个数
	"""
	用法：{% tag_multi x y z %}
	"""
	return x*y*z

举例：
<!--自定义过滤器-->
{{ 10|filter_multi:10 }} ==> 100
<!--假设 lic = [1,2]-->
{{ 2|filter_multi:lic }} ==> [1,2,1,2]

<!--自定义tag-->
{% tag_multi 3 5 10 %} ==> 150
```