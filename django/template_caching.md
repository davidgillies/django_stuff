

    TEMPLATE_LOADERS = (
        ('django.template.loaders.cached.Loader', (
            'django.template.loaders.filesystem.Loader',
            'django.template.loaders.app_directories.Loader',
        )), 
    )
    



This is not valid for Django 1.8 as the templating variables have changed. 
https://docs.djangoproject.com/en/1.8/ref/templates/api/
