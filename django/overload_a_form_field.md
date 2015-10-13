#Overloading a form field

To overload a form field use the following example

    from django import forms
    from django.core.exceptions import ValidationError
    
    class MyField(forms.IntegerField): # overload class of your choice
        default_error_messages = {'rangeerror': ('Entry must in range 10 - 50')}
        def validate(self, value):
            super(MyField, self).__init__(self, value):
            if value < 10 or value > 50:
                raise ValidationError(self.error_messages['rangeerror'], code='rangeerror')
                
                
##Usage

    m = MyField(5)
    try:
        m.clean(5)
    except ValidationError as e:
        error = unicode(e[0]) # get the actual error message
    print error
    
