Add to your settings.py:

  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
      },
      'db2': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': os.path.join(BASE_DIR, 'db2.sqlite'),
      },
      'db3': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': os.path.join(BASE_DIR, 'db3.sqlite'),
      },
      'db4': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': os.path.join(BASE_DIR, 'db3.sqlite'),
      },
      'db5': {
          'ENGINE': 'django.db.backends.sqlite3',
          'NAME': os.path.join(BASE_DIR, 'flasktaskr.db'),
      }
  }

  DATABASE_ROUTERS = ['shippees.routers.ShippeesRouter',
                    'yachts.routers.YachtsRouter',
                    'flasktasks.routers.FlaskTasksRouter',
                    ]
                    

and you need to add a routers.py file referenced in DATABASE_ROUTERS above, this one for shippees app:

  class ShippeesRouter(object):
      """
      A router to control all database operations on models in
      the myapp2 application
      """
 
      def db_for_read(self, model, **hints):
          """
          Point all operations on myapp2 models to 'my_db_2'
          """
          if model._meta.app_label == 'shippees':
              return 'db2'
          return None
 
      def db_for_write(self, model, **hints):
          """
          Point all operations on myapp models to 'other'
          """
          if model._meta.app_label == 'shippees':
              return 'db2'
          return None
 
      def allow_syncdb(self, db, model):
          """
          Make sure the 'myapp2' app only appears on the 'other' db
          """
          if db == 'db2':
              return model._meta.app_label == 'shippees'
          elif model._meta.app_label == 'shippees':
              return False
          return None

