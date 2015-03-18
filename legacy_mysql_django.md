## Setting up Django to use a legacy MySQL database

1. [Set up django to use pymysql](https://github.com/davidgillies/django_stuff/blob/master/django/mysql.md)
2. pip install pymysql
3. Set up the DATABASESin settings.py

            DATABASES = {
                 'default': {
                       'ENGINE': 'django.db.backends.sqlite3',
                       'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
                        },
                  'db2': {
                        'ENGINE': 'django.db.backends.mysql',
                        'NAME': 'sm_db',
                        'USER': 'david',
                        'PASSWORD': '****',
                        'HOST': 'localhost',
                        'PORT': '3306',
                  },
            }
      
Don't want all the usual django crap in our database so I've left it in sqlite.

4. You need to set up routers.py in your app folder to route the app to the right database:

      
            class PlayRouter(object):
                  """
                  A router to control all database operations on models in
                  the myapp2 application
                  """
 
                  def db_for_read(self, model, **hints):
                        """
                        Point all operations on myapp2 models to 'my_db_2'
                        """
                        if model._meta.app_label == 'rest_no_model':
                              return 'db2'
                        return None
 
                  def db_for_write(self, model, **hints):
                        """
                        Point all operations on myapp models to 'other'
                        """
                        if model._meta.app_label == 'rest_no_model':
                              return 'db2'
                        return None
 
                  def allow_syncdb(self, db, model):
                        """
                        Make sure the 'myapp2' app only appears on the 'other' db
                        """
                        if db == 'db2':
                              return model._meta.app_label == 'rest_no_model'
                        elif model._meta.app_label == 'rest_no_model':
                              return False
                        return None
              

5. In settings.py fot eh project:
      DATABASE_ROUTERS = ['rest_no_model.routers.PlayRouter',]

6. To create a models.py from the existing database:
      python manage.py inspectdb --database db2 > models.py
      
7. Do the migrations:
      python manage.py makemigrations
      python manage.py migrate
      
8. Set up your admin stuff as usual.


