#Overloading a form field

To overload a form field use the following example

    from django import forms
    from django.core.exceptions import ValidationError
    
    class MyField(forms.IntegerField): # overload class of your choice
        default_error_messages = {'rangeerror': ('Entry must in range 10 - 50')}
        def validate(self, value):
            super(MyField, self).__init__(self, value)
            if value < 10 or value > 50:
                raise ValidationError(self.error_messages['rangeerror'], code='rangeerror')
                
                
##Usage

    m = MyField()
    try:
        m.clean(5)
    except ValidationError as e:
        error = unicode(e[0]) # get the actual error message
    print error
    
#To compare several variables

Use a Form to set up the variables you will test.

    class MyForm(forms.Form):
        my_value = forms.IntegerField()
        min_value = forms.IntegerField()
        max_value = forms.IntegerField()

        def clean(self): # add a clean function to do extra validation.
            cleaned_data = super(MyForm, self).clean()
            my_value = cleaned_data.get('my_value')
            min_value = cleaned_data.get('min_value')
            max_value = cleaned_data.get('max_value')
            if my_value < min_value or my_value > max_value:
                raise forms.ValidationError(('Not in range %(min_value)s - %(max_value)s'), code='invalid', params={'min_value': min_value, 'max_value': max_value})
                
                
##Usage

    m = MyForm({'my_value': 5, 'min_value': 10, 'max_value': 50})
    if m.is_valid():
        for k,v in m.errors.items():
            print v # outputs form html
            print v[0] # just the text message.
