##Get it to log in admin screens
Install eventlog  

    pip install eventlog

Add to settings.py INSTALLED_APPS.
sync the database (python manage.py syncdb)
In your app/models.py, add:
    from eventlog.models import log
    
    class MyModel(models.Model):
      ...
      
      def save(self, *args, **kwargs):
          if not self.id:
              log(user=self.user, action='added', extra={'Name': self.name})
          else:
              log(user=self.user, action='updated', extra={'Name': self.name})
          super(Surgery, self).save(*args, **kwargs)
          
This will add events to the log whenever an instance of your model is saved.  In this case I am only passing the name of the model but you can pass what you like.  You can put whatever text you want in the action box as well.  This will no work in the admin screens.
##Using logs in public pages
In app/views.py

    from eventlog.models import Log
    
In your view function or class get the log stuff

    log_stuff = Log.objects.filter(user=request.user.id)
    

You need to pass this to the renderer in the queryset.  
3. Example template usage:

    {% for log in log_stuff%}
                        <li>
                            <a href="#">
                                <div>
                                    <i class="fa fa-tasks fa-fw"></i> {{log.extra.Name}} {{log.action}}
                                    <span class="pull-right text-muted small">{{log.timestamp|date:'H:i'}}</span>
                                </div>
                            </a>
                        </li>
                        <li class="divider"></li>
    {% endfor %}
