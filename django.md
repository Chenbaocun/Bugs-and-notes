# Django 学习笔记
1. **避免在ORM中使用get，用filter——if——for代替**
- 返回空
- 可能返回多个
2. **QuerySet对象有以下几个方法**
- first()
- last()
- count()
- value() 整合成[{key : value}] ,配合Jason.dunp()进行转换
- exist()
3. **QuerySet可以进行切片[]，和Python惯例一样左闭右开**
- 但是这个并不是查出来再进行切片的，这对大量的数据是不可能的，会转换成对应的sql语句，完成指定的查询
- 也不能用函数
4. **ORM并不是立即执行的（缓存集，又称懒查询）**
- 只有当我们调用查询出出来的queryset的时候才会去执行增删改查
5. **对时间进行查询时，可能会出现问题**
- 未知的时区问题，可以把Settings.py 中的 use_tz = FALSE了
6. **查询也有聚集函数Max，Min，Avg等等**
cls.object.aggregate(Max('字段名'))。 结果是dict{key:value}
7. **F对象：同一个表内的不同字段进行比较（比如查询男生比女生多的公司）**
company = Company.object.filter(c_boy_num_lt = F('c_girl_num') - 15) #女生比男生多15个以上
8. **Q对象：对已有条件进行封装，使得多个查询条件可以 & | ~**
- 多个fiter的另一种写法
company = Company.object.filter(Q('c_girl_num_gt=1') & Q('c_girl_num_lt=10'))
9. **model的属性**
- 显示属性
  - 用户自己声明的属性
- 隐式属性
  - 没有书写，ORM自动生成的。 比如默认 object = models.Manager ，如果自己改了 a = models.Manager ，我们在进行cls.object(替换成a).filter()进行计算了
  - 如果自己声明了，或者叫重写了，系统就不会自动生成了
10. **如果想更改filter的逻辑，可以重写models的manager**
'''python3
class MyManager(models.Manager):
def get_qyeryset(self):
    return super(MyManager, self).get_qyeryset().filter(is_delete = False)
'''
- 使得所有调用get_queryset 的方法都 不会查到已经逻辑删除的数据
- 这种方式只适合逻辑删除这样的操作，其他的操作会产生其他的逻辑后果。
11. **静态资源**
- 创建static文件夹
- 在settings.py中进行注册
  - ```python3
  STATIC_PATH = os.path.join(BASE_DIR, 'static')
  STATICFILES_DIRS = (
    STATIC_PATH,
) ```
- 在模板中使用:先加载{%load static%},引用时{%static '/css/xxx.css'%}
- 但是此种方式只能在debug模式下使用，关闭后将无法使用，使用其他的服务器如Nginx对静态资源进行管理。
12. **状态码（4开头的都是客户端错了）**
- 200：
- 404：资源未找到，如果想改写页面，可以在template文件夹下编写404.html即可。Django内部其实都有这样的默认页面，我们只是重写了而已。
- 403：禁止访问
- 400：
- 500：服务器内部错误。
13. **request.META**
14. **request**
- method
- Get
  - 类字典结构
  - 一个key对应多个value
  - get('name')
  - getist('name') #获得所有的key='name'对应的值
- Post
  - 与Get类似
- Meta
  - 客户端的各种信息，ip，又或者主机的用户名。
- File
  - 与文件上传相关
15. **Response**
- HttpResponse的属性
  - content：要返回的内容。
  - status_code：返回状态码（页面就算是正常访问了，也可以返回404，可以一定程度上骗爬虫）。
  - charset:编码格式，如utf-8
  - content-type：MIME类型，传输的文件类型，使浏览器可以调用合适的程序打开这些文件。
16. **Nginx**
- 负载均衡，反向代理，高并发，轻量级服务器
- jd，淘宝，网易等都在用。
