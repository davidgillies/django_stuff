1. pip install djangorestframework
2. Add 'rest_framework' to INSTALLED_APPS in settings.py.
3. Might need the following:

        REST_FRAMEWORK = {
          'DEFAULT_PERMISSION_CLASSES': ('rest_framework.permissions.IsAdminUser',),
          'PAGE_SIZE': 10
        }

        TEMPLATE_CONTEXT_PROCESSORS = (
          'django.contrib.auth.context_processors.auth',
          'django.core.context_processors.request',
        )

4. In views.py add:

        from rest_framework.views import APIView
        from rest_framework.response import Response
        from rest_framework import status
        
        # in your view
        def my_view(request):
            my_dict = {'some_data': 4}
            response = Response(my_dict, status=status.HTTP_200_OK)
            return response
            
5. This works fine for any dict.  There are a number of status options e.g.
status.HTTP_204_NO_CONTENT for delete
status.HTTP_201_CREATED for post etc.
