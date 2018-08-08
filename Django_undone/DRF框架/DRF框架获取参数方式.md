# DRF获取参数的方式 #

----------


例如url
`url(r'^demo/(?P<word>.*)/$', DemoView.as_view())`

## 在类视图中获取参数 ##
url:`http://127.0.0.1:8000/demo/aaa/?bbb=bbb&ccc=ccc&ccc=CCC`
form:`{"body":"body"}`
JSON:`{"body":"body"}`

```python
class DemoView(APIView):

	def post(self, request, aaa):
		aaa = aaa  # 获取url路径中的参数
		bbb_str = request.query_params.get('bbb')  # 获取一个查询字符串的参数
		ccc_list = request.query_params.getlist('ccc')  # 获取多个查询字符串参数
		# 请求体中的参数
		# 如果通过form表单传递,获取出来是QueryDict,通过.dict()转换成python的字典
		form_body = request.data
		# 如果通过JSON传递,获取出来就是字典,例如{'body':'body'}
		# json_body = request.data
		print(aaa)
		print(bbb_str)
		print(ccc_list)
		print(form_body.dict())
		# print(json_body)
		return Response({'message': 'OK'})
```
结果
```python
aaa
bbb
['ccc', 'CCC']
{'body': 'body'}
```

URL路径参数/查询字符串不区分请求方式,GET/POST/PUT等都一样


## serializer中获取参数 ##

```python
# view
class DemoView(GenericAPIView):
	serializer_class = DemoSerializer

	def post(self, request, aaa):
		serializer = self.get_serializer(data=request.query_params)
		serializer.is_valid(raise_exception=True)
		return Response({'message': 'OK'})

# serializer
class DemoSerializer(serializers.Serializer):
	bbb = serializers.CharField()
	ccc = serializers.ListField()  # List

	def validate(self, attrs):
		aaa = self.context['view'].kwargs.get('aaa')  # 获取路径参数
		bbb = attrs['bbb']  # 获取查询字符串
		ccc = attrs['ccc']  # 获取以多个key相同的查询字符串
		# 获取当前登陆的对象,需要根据场景进行使用
		# user = self.context['request'].user
		print(aaa)
		print(bbb)
		print(ccc)
		return attrs
```