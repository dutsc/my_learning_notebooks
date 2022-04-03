# python爬虫







## 内置urllib库的使用

1. 导入所需库

   ```python
   from urllib import request
   ```

   若有需要，则进行取消证书验证 

   ```python
   import ssl
   ssl._create_default_https_context = ssl._create_unverified_context
   ```

2. 准备url地址，创建请求对象

   ```python
   url = "https://www.baidu.com"
   req = request.Request(url)
   ```

3. 发送请求，并返回response响应对象

   ```python
   res = request.urlopen(url)
   ```

4. 输出响应状态码

   ```python
   print(res.status)
   ```

5. ```python
   import re
   html = res.read().decode("utf-8")
   #输出网页标题
   print(re.findall("<title>(.*?)</title>",html))
   ```

   
