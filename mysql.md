## Using a MySQL backend with pymysql

Add into your manage.py:

try:
    import pymysql
    pymysql.install_as_MySQLdb()
except ImportError:
    pass 
    

In your settings.py:

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'new_schema',
        'USER': 'david',
        'PASSWORD': 'david',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
