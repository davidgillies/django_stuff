Install:

    pip install django-adminplus
    

Add to apps:

    INSTALLED_APPS = (
        # ...
        'adminplus',
        # ... 
    )
    
Also replace 'django.contrib.admin' in INSTALLED APPS with:

            'django.contrib.admin.apps.SimpleAdminConfig',

Add to urls.py:

    from django.contrib import admin
    from adminplus.sites import AdminSitePlus

    admin.site = AdminSitePlus()
    admin.autodiscover()
    
Replace django.contrib.admin with django.contrib.admin.apps.SimpleAdminConfig in INSTALLED_APPS.

Now in admin.py:

    def my_view(request, *args, **kwargs):
        HttpResponse('hello')
    admin.site.register_view('somepath', view=my_view)
    
This adds a Custom Views box to the admin views with a link to /admin/somepath

