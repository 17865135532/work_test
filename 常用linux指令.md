1、端口占用的问题

​	netstat -tlnp|grep 8004
​	kill -9 进程id

2、redis 链接

redis-cli -h 192.168.2.177 -p 26379

auth 密码

3、ssh 链接



3、MongoEngine 操作

```
MongoEngine是基于Python的对象系统设计的MongoDB专用的ORM框架。与SQLAlchemy不同的是，MongoEngine会自动生成一个唯一的标识，用ID属性表示。当然MongoEngine与SQLAlchemy还有很对不同的地方，比如字段类型等。
```

4、mongoEngine 所支持的操作符

操作符的表示形式为:加在关键字后面使用"__+操作符"(此处是两个" _ "),例如：publish_data__gt

```
ne：不等于
lt：小于
lte：小于或等于
gt：大于
gte：大于或等于
not：对一个操作符取否，例如publish_data__not__gt
in：值在列表中
nin：值不在列表中
mod：值%a==b,a和b用(a,b)的方式传递
all：列表中的所有值都在该字段中
size：列表的大小
existes：在该字段中存在这个值

作者：QuiryRain
链接：https://www.jianshu.com/p/869fe8a668d4
来源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。
```

5、检测字符串的部分操作符

```
exact：字符串相等
iexact：字符串相等（大小写不敏感）
contains：字符串包含该值
icontains：字符串包含该值（大小写不敏感）
startswith：字符串以该值开始
istartswith：字符串以该值开始（大小写不敏感）
endswith：字符串以该值结束
iendswith：字符串以该值结束（大小写不敏感）

```

6、可以对字段值进行修改的操作符

```
set：设置一个值
unset：删除一个值
inc：将值自增
dec：将值自减
push：把一个值加到列表的末尾
push_all：把几个值加到列表的末尾
pop：移除列表中的第一个或者是最后一个值
pull：移除列表中的值
pull_all：移除列表中的几个值
add_to_set：当且晋档某值不在列表中时，将其添加进列表
```







3、Python中使用mongoengine
（1）链接
from mongoengine import *
from datetime import datetime

###### 连接数据库

connect('blog') # 连接本地blog数据库
如需验证和指定主机名
connect('blog', host='192.168.3.1', username='root', password='1234')

##### 定义分类文档
class Categories(Document):
 ' 继承Document类,为普通文档 '
 name = StringField(max_length=30, required=True)
 artnum = IntField(default=0, required=True)
 date = DateTimeField(default=datetime.now(), required=True)

（2）插入
cate = Categories(name="Linux") # 如果required为True则必须赋予初始值,如果有default,赋予初始值则使用默认值
cate.save() # 保存到数据库
（3）查询和更新
##### 返回集合里的所有文档对象的列表
cate = Categories.objects.all()

##### 返回所有符合查询条件的结果的文档对象列表
cate = Categories.objects(name="Python")
##### 更新查询到的文档:
cate.name = "LinuxZen"
cate.update()

###### （4）ReferenceField 引用字段:

通过引用字段可以通过文档直接获取引用字段引用的那个文档:
class Categories(Document):
 name = StringField(max_length=30, required=True)
 artnum = IntField(default=0, required=True)
 date = DateTimeField(default=datetime.now(), required=True)

class Posts(Document):

 title = StringField(max_length=100, required=True)
 content = StringField(required=True)
 tags = ListField(StringField(max_length=20, required=True), required=True)
 categories = ReferenceField(Categories)
（5）插入引用字段
cate =Categories(name="Linux")
cate.save()
post = Posts(title="Linuxzen.com", content="Linuxzen.com",tags=["Linux","web"], categories=cate)
post.save()
（6）通过引用字段直接获取引用文档对象
cate = Posts.objects.all().first().categories
cate
cate.nam
（7）EmbeddedDocument 嵌入文档




