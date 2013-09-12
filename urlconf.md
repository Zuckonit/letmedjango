##Django URLConf

[参考资料](http://www.cnblogs.com/BeginMan/archive/2013/03/21/2973820.html)  

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
        from mysite.models import MyModel
        
        def foobar_view(request, url):
            m_list = MyModel.objects.filter(is_new=True)
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

