# 模板控制语句&模板标签Tags

### 控制语句(if & for)
#### if
```
{% if 1 > 2 %}
{# 注意比较运算符两边都要有空格，否则报错 #}
	<p>false</p>
{% else %}
	<p>1大于2是false的</p>
{% endif %}
{# {% elif %}(举例略) #}
```
#### for    
```
{% for val in 'abcd' %}
	{% if forloop.first %}
		我是第一次我骄傲~<br>
	{% endif %}
	索引1（从1开始）：{{ forloop.counter }} ||
	索引2（从0开始）：{{ forloop.counter0 }} ||
	反转索引1：{{ forloop.revcounter }} ||
	反转索引2：{{ forloop.revcounter0 }} ||
	val：{{val}} ||
	{{ forloop.first }}<br>
{% endfor %}
{# forloop.first某些场景很有用，循环的第一次的时候值为True #}

HTML输出：
我第一我骄傲~
索引1（从1开始）：1 || 索引2（从0开始）：0 || 反转索引1：3 || 反转索引2：2 || val：a || True 
索引1（从1开始）：2 || 索引2（从0开始）：1 || 反转索引1：2 || 反转索引2：1 || val：b || False 
索引1（从1开始）：3 || 索引2（从0开始）：2 || 反转索引1：1 || 反转索引2：0 || val：c || False 
```
### 标签Tags

#### empty
```
<!--应用场景：列表或元组等可迭代元素为空时判断输出-->
{%for i in '' %}
	<p>我要输出i变量{{i}}</p>
{%empty%}
	<p>i里面是空的哦</p>
{%endfor%}
```
#### with：变量名重命名
```
<!--with把长变量名称变成短名称，仅限于with块内部使用-->
{% with bianduan=wocanidayebianliangmingzizhemechang %} {{ bianduan }} {% endwith %}
```
#### verbatim：禁止渲染
```
{% verbatim %} {{ 变量 }} {% endverbatim %}

HTML原封不动直接输出：{{ 变量 }}
```
#### load：加载tags库
```
需要在应用下先创建一个 templatetags 库，里面写一些自定义的tags或者filter，文件命名方式：自定义_tags.py 

导入自定义tags库：{% load my_tags %}
引入静态文件：
{% load staticfiles %}
<script type="text/javascript" src="{% static 'js/jquery-3.3.1.min.js' %}"></script>
```