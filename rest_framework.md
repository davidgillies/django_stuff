    pip install djangorestframework
    
After installing:
1. Add rest_framework to your INSTALLED_APPS in settings.py
2. You can add other options in settings.py such as:

    REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': ('rest_framework.permissions.IsAdminUser',),
    'PAGINATE_BY': 10
    }
    

3. Create a serializers.py file in your app and add in classes for all the models you want in the api, e.g.:

    	class VolunteerSerializer(serializers.HyperlinkedModelSerializer):
        	class Meta:
            	model = Volunteer
            	exclude = ("user",)


    	class AppointmentSerializer(serializers.HyperlinkedModelSerializer):
        	class Meta:
            	model = Appointment


    	class SurgerySerializer(serializers.HyperlinkedModelSerializer):
        	class Meta:
            	model = Surgery


		class GPSerializer(serializers.HyperlinkedModelSerializer):
        	class Meta:
            	model = GP
            

4. In your apps urls.py add in the router urls, I think there are more ways of doing this, e.g.:

    	from rest_framework.routers import DefaultRouter
    	router = DefaultRouter()
    	router.register(r'volunteers', views.VolunteerViewSet)
    	router.register(r'appointments', views.AppointmentViewSet)
    	router.register(r'surgeries', views.SurgeryViewSet)
    	router.register(r'gps', views.GPViewSet)
	urlpatterns = patterns('',
        		url(r'^$', 'study_manager.views.index', name='index'), 
        		url(r'^api/', include(router.urls)),
    	)

5. In views.py, need to add in views, there are other ways to do this too e.g.:

    	from rest_framework import viewsets
    	from rest_framework.decorators import api_view
    	from rest_framework.response import Response
    	from rest_framework.reverse import reverse
    
    	@api_view(('GET',))
    	def api_root(request, format=None):
		return Response({
	        'appointments': reverse('appointment-list', request=request, format=format),
      		'volunteers': reverse('volunteer-list', request=request, format=format),
        	'surgeries': reverse('surgery-list', request=request, format=format),
            	'gps': reverse('gps-list', request=request, format=format),
        	})


    	class VolunteerViewSet(viewsets.ModelViewSet):
        	"""
        	This viewset automatically provides `list`, `create`, `retrieve`,
        	`update` and `destroy` actions.
		
        	Additionally we also provide an extra `highlight` action.
        	"""
        	queryset = Volunteer.objects.all()
        	serializer_class = VolunteerSerializer
        	
        	
        class SurgeryViewSet(viewsets.ModelViewSet):
        	"""
        	This viewset automatically provides `list` and `detail` actions.
        	"""
        	queryset = Surgery.objects.all()
        	serializer_class = SurgerySerializer
        	
        	
    	class GPViewSet(viewsets.ModelViewSet):
        	"""
        	This viewset automatically provides `list` and `detail` actions.
        	"""
        	queryset = GP.objects.all()
        	serializer_class = GPSerializer
        	
        	
	class AppointmentViewSet(viewsets.ModelViewSet):
        	"""
        	This viewset automatically provides `list` and `detail` actions.
        	"""
        	queryset = Appointment.objects.all()
        	serializer_class = AppointmentSerializer
        	
Think that's it!!
