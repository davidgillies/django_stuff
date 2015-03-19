from django.forms.models import model_to_dict
import simplejson

json_dict = simplejson.JSONDecoder().decode(body) # body is json from request.body
data = model_to_dict(Volunteer.objects.get(volunteer_id=id_variable_value)) # model to dict

Volunteer.objects.create(**json_dict) # create a model from a dict
Volunteer.objects.filter(pk=id_variable_value).update(**json_dict) # update a model from a dict
