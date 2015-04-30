In models.py add your model:

    class MyTemplate(models.Model):
        content = models.TextField()
    

In admin.py connect model to admin:
    
    class MyTemplateAdmin(admin.ModelAdmin):
        pass

    admin.site.register(MyTemplate, MyTemplateAdmin)

In views.py:

    from django.shortcuts import render
    from django.template import Template, Context
    from .models import MyTemplate
    from django.http import HttpResponse


    def db_tpl(request):
        t = MyTemplate.objects.get(pk=1) # need to go to admin and add your first template.
        tpl = Template(t.content) # takes your template text and compiles to a template
        context = Context({'a':'hello', 'b': 'world'}) # convert whatever data you use to a context object
        return HttpResponse(tpl.render(context)) # 
    

    
