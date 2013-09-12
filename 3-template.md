##Django模版引擎
* 什么是模版  
    * Django有自带的模版引擎， 但第三方的模版引擎还有很多
    * 所谓模版引擎， 个人的理解就是在网页中需要动态改变的地方做个标记， 通过Controller或者Controller与Models的交互来动态改变标记内容

* Django模版设置

    ```
    通常可以用下面的这样一句代码来设置你的模版的根目录， 修改TEMPLATE_DIRS的值
    #settings.py
    
    TEMPLATE_DIRS = (  
        os.path.join(os.path.dirname(__file__), 'templates').replace('\\','/'),  
    )  
    ```

* 模版的使用
    * string作为模版(这个固然不推荐， 只是用来解释模版的使用)
    
    ```
    from django.http import HttpResponse
    from djang.template import Template, Context
    import datetime
    
    def curdate(request):
        t = Template('<html><body>now is {{cur_date}}</body></html>')
        c = Context({'cur_date': datetime.datetime.now()})
        html = t.render(c)
        return HttpResponse(html)
    ```
    
    * 载入模版的方式  
        * 通过刚刚Django的模版设置， 我们可以把模版写到这个目录里面去。
        
        ```
        #date.html
        <html>
            <body>
                now is {{cur_date}}
            </body>
        </html>
        ```

        ```
        from django.shortcuts import render_to_response
        import datetime
        
        def curdate(requeset):
            cur_date = datetime.datetime.now()
            return render_to_response('date.html', {'cur_date': curdate})
            #或者用一个trick
            #return render_to_response('date.html', locals())
        ```
        
    * 模版语法
        * 至于模版的语法， 这个可以去看[官方文档](https://docs.djangoproject.com/en/dev/topics/templates/)， 不在累赘叙述
        * 官方给的内建模版中可使用的[tag和filter](https://docs.djangoproject.com/en/dev/ref/templates/builtins/)
