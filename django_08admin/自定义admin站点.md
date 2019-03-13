# 自定义admin站点
```

#coding:utf-8
from django.contrib import admin

from orm import models

class UserAdmin(admin.ModelAdmin):
	"""在admin站点中自定制显示记录信息"""
	list_display = ('id','username','password','reg_date','user_role')
	list_editable = ('username','user_role')
	# filter_horizontal = ('user_role',) #水平过滤，多对多关系字段的设置，设置了之后，选择的时候就可以模糊查询还能多选
	# filter_vertical = (,) #垂直过滤
	list_per_page = 10
	search_fields = ('id','username','user_role__rolename')  #不适用多对多的字段，一对多的字段要注意，例：user_role__rolename
	list_filter = ('reg_date','user_role')
	ordering = ('-reg_date','id') #日期降序，加个-代表降，如果第一个字段值一样，则按第二个排序，后面再加以此类推

	fieldsets = [
		(None, {'fields':['username']}), #None代表默认，添加或编辑记录时，默认显示的编辑字段
		('其他信息',{'fields':['reg_date','user_role'], 'classes':['collapse']}),#这里面显示的是有默认值的字段，classes=collapse是设置前面的fields是否展示出来，主要是样式上的
	]


# 将你的表注册到Django的admin管理平台中
admin.site.register(models.User, UserAdmin)
admin.site.register(models.Role)


```