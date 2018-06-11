# flask基础-模板-表单 #

使用模板的好处：

视图函数只负责业务逻辑和数据处理(业务逻辑方面)
而模板则取到视图函数的数据结果进行展示(视图展示方面)
代码结构清晰，耦合度低

渲染模版函数:
`render_template(template_name_or_list, **context)`

参数:
`template_name_or_list`:模板名,或者是包含模板名的列表,自动使用第一个作为模板.
`**context`:以key-value形式保存传入模板的的数据,key为模板中使用变量名,value为数据(或者是保存的变量)

变量代码块:形如`{{变量名}}`,数据类型不限

## 过滤器: ##

在模板中对数据进行处理(格式化输出),本质上就是模板引擎中的函数.

调用方式:`{{ 变量名 | 过滤器名(参数) }}` 支持链式调用

常用过滤器:

| 字符串过滤器 | 介绍 |  |
| --- | --- | --- |
| safe | 禁止转义,html标签将直接输出,不会转义(比如'<'不会转义&lt) |  |
| capitalize | 首字母大写 |  |
| lower | 全部小写 |  |
| upper | 全部大写 |  |
| title | 标题化,全部单词的首字母大写 |  |
| reverse | 字符串反转 |  |
| format | 格式化输出 |  |
| striptags | 去除html标签 |  |
| truncate | 字符串截断,切片 |  |
|  |  |  |
| 列表过滤器 |  |  |
| first | 取出第一个 |  |
| last | 取出最后一个 |  |
| length | 列表长度 |  |
| sum | 列表内数值求和 |  |
| sort | 排序,默认升序 |  |

自定义过滤器:
```python
# 第一种,装饰器方式
@app.template_filter('lireverse')  # lireverse是过滤器调用时的名字
def do_listreverse(li):
    temp_li = list(li)
    temp_li.reverse()
    return temp_li


# 第二种,直接添加
def do_listreverse(li):
    temp_li = list(li)
    temp_li.reverse()
    return temp_li

app.add_template_filter(do_listreverse,'lireverse')

```

## 控制代码块 ##

**if-else**
语法:
```
{% if 条件 %}
    ...
{% elif %}
    ...
{% else %}
    ...
{% endif %}
```

**for循环**
```
{% for x in x_list if 条件 %}
    ...
{% endfor %}
```

关于loop

| 属性 | 介绍 |
| --- | --- | 
| loop.index	| 当前循环迭代的次数（从 1 开始）| 
| loop.index0	| 当前循环迭代的次数（从 0 开始）| 
| loop.revindex	| 到循环结束需要迭代的次数（从 1 开始）| 
| loop.revindex0	| 到循环结束需要迭代的次数（从 0 开始）| 
| loop.first	| 如果是第一次迭代，为 True 。| 
| loop.last	| 如果是最后一次迭代，为 True 。| 
| loop.length	| 序列中的项目数。| 
| loop.cycle	| 在一串序列间期取值的辅助函数。见下面示例程序。| 

## 模板的复用 ##

**宏(macro)**:相当于就是一个函数,封装了html模板中的代码的块.

定义,单独保存为一个html页面
```python
{% macro bbb(name,value='',type='text') %}
    <input type="{{type}}" name="{{name}}" value="{{value}}" class="form-control">
{% endmacro %}
```
导入:`{% import 'macro.html' as aaa %}`
调用:`{{ aaa.bbb() }}`


**继承**:

不支持多继承,block中的块名字不能相同,最好block首尾都写块名字.

在**父模板**中定义,father.thml
```
{% block 块名字 %}
    ...
{% endblock 块名字 %}
```

在**子模板**中继承方式,son.html:
```
{% extends 'father.html' %}

{% block 块名字 %}
    ...  # 新内容
{% block content %}
```

**包含**(include):就是可以在其他html中直接调用固定的html文件的方法

方式:`{% include 'xxx.html' ignore missing %}`
设置`ignore missing`参数,当include的html文件不存在时不会报错,而是直接忽略.


FORM表单
需要安装: Flask-WTF

操作步骤:
1.导入模块
2.创建表单类
3.在视图中创建表单实例并渲染返回给浏览器
4.当表单输入内容满足要求则在视图中接收数据,不满足时另做处理.

```
# 导入wtf扩展的表单类
from flask_wtf import FlaskForm
# 导入自定义表单需要的字段
from wtforms import SubmitField,StringField,PasswordField
# 导入wtf扩展提供的表单验证器
from wtforms.validators import DataRequired,EqualTo

# 设置secret_key
app.config['SECRET_KEY']='任意加密内容'

# 定义自定义的表单类,继承FlaskForm基类
class RegisterForm(FlaskForm):
    username = StringField("用户名：", validators=[DataRequired("请输入用户名")], render_kw={"placeholder": "请输入用户名"})
    password = PasswordField("密码：", validators=[DataRequired("请输入密码")])
    password2 = PasswordField("确认密码：", validators=[DataRequired("请输入确认密码"), EqualTo("password", "两次密码不一致")])
    submit = SubmitField("注册")

@app.route('/demo2', methods=["get", "post"])
def demo2():
    # 创建表单对象,实例化
    register_form = RegisterForm()
    # 提交表单时调用validate_on_submit(),当表单类中的validators都验证通过才能往下执行.
    if register_form.validate_on_submit():
        # 获取表单数据
        username = request.form.get("username")
        password = request.form.get("password")
        password2 = request.form.get("password2")
        # 对数据进行处理
        print(username, password, password2)
        return "success"
    else:
        if request.method == "POST":
            flash("参数有误或者不完整")

    return render_template('temp_register.html', form=register_form)

```

**常用字段**:

| 表单字段 | 介绍 |
| --- | --- |
| **StringField** | 文本字段 |
| **TextAreaField** | 多行文本字段 |
| **PasswordField** | 密码文本字段 |
| HiddenField | 隐藏文件字段 |
| DateField | 文本字段，值为 datetime.date 文本格式 |
| DateTimeField | 文本字段，值为 datetime.datetime 文本格式 |
| **IntegerField** | 文本字段，值为整数 |
| DecimalField | 文本字段，值为decimal.Decimal |
| FloatField | 文本字段，值为浮点数 |
| **BooleanField** | 复选框，值为True 和 False |
| **RadioField** | 一组单选框 |
| **SelectField** | 下拉列表 |
| **SelectMutipleField** | 下拉列表，可选择多个值 |
| **FileField** | 文件上传字段 |
| **SubmitField** | 表单提交按钮 |
| FormField | 把表单作为字段嵌入另一个表单 |
| FieldList | 一组指定类型的字段 |

**常用的验证函数**:

| 验证函数 | 介绍 |
| --- | --- |
| **DataRequired** | 确保字段中有数据 |
| **EqualTo** | 比较两个字段的值，常用于比较两次密码输入 |
| **Length** | 验证输入的字符串长度 |
| **NumberRange** | 验证输入的值在数字范围内 |
| URL | 验证URL |
| AnyOf | 验证输入值在可选列表中 |
| NoneOf | 验证输入值不在可选列表中 |

