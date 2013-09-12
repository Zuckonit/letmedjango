##Django URLConf

[参考资料](http://www.cnblogs.com/BeginMan/archive/2013/03/21/2973820.html)  

*  设置  
```
#settings.py
ROOT_URLCONF=xxxx         #该参数告诉Django用作本站的ULRConf, 默认是urls.py
```

* Django 处理请求的工作机制, 路由器
    * 服务器启动， Django去同目录下的settings.py文件里寻找ROOT_URLCONF, 即寻找URLConf文件
    * 访问url的时候， Django根据ROOT_URLCONF装载URLConf
    * 逐个匹配urlpatterns, 命中即调用关联的视图函数，并HttpRequest对象作为第一个参数(也就是request参数)
    * 最后view函数负责返回一个HttpResponse对象, 呈现给浏览器
    * ![dispatcher](http://images.cnitblog.com/blog/476998/201303/21173739-ca2d6fac22d44a52ae159be2ebf0a00c.png)


*  不传参  
```
from django.conf.urls.defaults import *
from views import hello
import views
urlpatterns = patterns('',
        (r'^hello/', hello),
        (r'^hello1/', views.hello),
        (r'^hello2/', 'demo.view.hello'), #视图字符串路径， 不需要导入模块
)
```  

*  传参  
    * 动态传参
    
    ```
    #views.py
    def hello(request, year, month):
        #do something here
        pass
    ```

    ```
    from django.conf.urls.defaults import *
    from views import hello
    urlpatterns = patterns('',
           (r'^arcticles/(?P<year>\d{4})/(?P<month>\d{2})/$', veiws.month_archive),  #命名组对应视图参数
    )
    ```

    * 固定参数
   
    ```
    #urls.py
    from django.conf.urls.defaults import *
    from mysite import views

    urlpatterns = patterns('',
        (r'^foo/$', views.foobar_view, {'template_name': 'template1.html'}),
        (r'^bar/$', views.foobar_view, {'template_name': 'template2.html'}),
    )
    ```
    
    ```
    from django.shortcuts import render_to_response
    from mysite.models import MyModel
    def foobar_view(request, template_name):
        m_list = [1,2,3]
        return render_to_response(template_name, {'m_list': m_list})
    ```
*  视图冗余  
```
#urls.py
from django.conf.urls.defaults import *
from mysite import views
urlpatterns = patterns('',
    (r'^(foo)/$', views.foobar_view),
    (r'^(bar)/$', views.foobar_view),
)
```

```      
# views.py
from django.shortcuts import render_to_response

def foobar_view(request, url):
    m_list = [1,2,3]
    if url == 'foo':
    template_name = 'template1.html'
    elif url == 'bar':
    template_name = 'template2.html'
    return render_to_response(template_name, {'m_list': m_list})
```            

*  include导入

```
from django.conf.urls.defaults import *
urlpatterns = patterns('',
   (r'^weblog/', include('mysite.blog.urls')),
)
此时， 访问的link变为^weblog/前缀 + 加上include的urls里面的设置
```
