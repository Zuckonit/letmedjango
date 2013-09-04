![django](django-logo.jpg)
##What is Django
A web framework written in python.  
Fast  
Light  


##Let's start
###Develop environment setup (of mine)
* Install virtualenv (problem caused by different version can be perfect solved by this)
    *  sudo pacman -S python2-virtualenv
    *  virtualenv env (create a virtual environment called 'env' for python)      
    *  source env/bin/active (load the virtual env)
    *  pip install django (install django)
* Choose Editor  
    *  vim + pydiction (recommend)
           + install vim
           + install pydiction plugin
           + django-admin.py startproject myfirstdjango
           + cd myfirstdjango
           + export DJANGO_SETTINGS_MODULE=settings
           + cd <the path of setting.py>
           + export PYTHONPATH=`pwd`
           + python pydiction.py django django.conf django.contrib django.core django.db django.dispatch django.forms django.http django.middleware django.shortcuts django.template django.templatetags django.utils django.views django.db.models
           + finally, let g:pydiction_location='/path/to/complete-dict'
           + enjoy it
    *  pycharm
  
##Hello world
* django-admin.py help (tool of django)
* django-admin.py startproject firstdjango (create a django project)
* cd firstdjango 
* python manage.py runsever
* open your browser, it works

