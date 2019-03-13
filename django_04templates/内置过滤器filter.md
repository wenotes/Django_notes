# filter 常用过滤器
**语法格式:{{ obj|filter:arg }}  obj是对象也可以是变量**

```
<!--safe:标记一个字符串是安全的。也就是会关掉这个字符串的html自动转义。类似模板标签中的{% autoescape off %}-->
{{ '<h1>abc</h1>'|safe }} ==> abc (h1大小的)

<!--date:将一个日期按照指定的格式，格式为字符串。-->
假设后端传过来是：d = datetime.datetime.now()
{{ d|date:'Y-m-d' }} ==> 2019-03-13
```
<table><thead><tr><th align="center">格式字符</th><th align="center">描述</th><th align="center">示例</th></tr></thead><tbody><tr><td align="center">Y</td><td align="center">四位数字的年份</td><td align="center">2019</td></tr><tr><td align="center">m</td><td align="center">两位数字的月份</td><td align="center">01-12</td></tr><tr><td align="center">d</td><td align="center">两位数字的天数</td><td align="center">01-31</td></tr><tr><td align="center">n</td><td align="center">月份，无0前缀</td><td align="center">1-12</td></tr><tr><td align="center">j</td><td align="center">天数，无0前缀</td><td align="center">1-31</td></tr><tr><td align="center">h</td><td align="center">小时，12小时制，有0前缀</td><td align="center">01-12</td></tr><tr><td align="center">g</td><td align="center">小时，12小时制，无0前缀</td><td align="center">1-12</td></tr><tr><td align="center">H</td><td align="center">小时，24小时制，有0前缀</td><td align="center">01-24</td></tr><tr><td align="center">G</td><td align="center">小时，24小时制，无0前缀</td><td align="center">1-24</td></tr><tr><td align="center">i</td><td align="center">分钟，有0前缀</td><td align="center">00-59</td></tr><tr><td align="center">s</td><td align="center">秒，有0前缀</td><td align="center">00-59</td></tr></tbody></table>  

```
<!--add 给变量加上相应的值-->
{{ 3|add:2 }} ==>5

<!--cut:移除字符串中所有指定的字符串,类似python中的replace(args,"")-->
{{ 'a,b,c'|cut:',' }} ==> abc

<!--join将列表/元组/字符串用指定的字符进行拼接,类似python的join-->
{{ 'abc'|join:'->' }} ==> a->b->c

<!--slice：类似python中的切片操作-->
{{ 'abcdefg'|slice:'1:3' }} ==> bc

<!--truncatewords==>和slice有区别，显示前面 "几个元素" ，然后后面用省略号代替.-->
后端传过来 var = ['a','b','c']
{{ var|truncatewords:"2" }} ==> ['a','b'...

<!--truncatechars: 如果给定的字符串长度超过了过滤器指定的长度。那么会进行切割，并且拼接三个点来作为省略号-->
后端传过来 var = ['a','b','c']
{{ var|truncatechars:"6" }} ==> ['a...  #这三个点加上转成字符串自己的那部分等于6

<!--truncatechars_html: 会忽略字符串中的html标签，其他同truncatechars-->

<!--length：将列表/元组/获取一个列表/元组/字符串/字典的长度。value为None，则返回0 -->
{{ 'abcdefg'|length }}  ==> 7

<!--floatformat:四舍五入的方式格式化一个浮点数类型-->
- 如果这个过滤器没有传递任何参数
- 只会保留一个小数
- 若小数全为0，则只保留整数
- 如果传递参数，则标识具体要保留几个小数

<!--default ：如果value是一个比如 []{},None,"" 等在if中被认为是False的值，可以使用default够提供的默认值-->
{{ ''|default:'苍井空' }} ==> 苍井空

<!--default_if_none：仅仅当value为None才会使用后面提供的值-->
{{ None|default:'这是None' }} ==> 这是None

<!--first:返回列表/元组/字符串的第一个元素-->
{{ 'abc'|first }} ==> a

<!--last:返回列表/元组/字符串的最后一个元素-->
{{ 'abc'|last }} ==> c

<!--striptags：删除字符串中所有的html标签-->
{{ '<h1>abc</h1>'|striptags  }} ==> abc

<!--urlencode：urlencode编码-->
{{ '小明'|urlencode }} ==>%E5%B0%8F%E6%98%8E

<!--lower：转小写-->
{{ 'ABC'|lower }} ==>abc

<!--upper：转大写-->
{{ 'abc'|upper }} ==>ABC

<!--random：在被给的列表/字符串/元组中随机的选择一个值-->
{{ 'abcdefg'|random }}

```

