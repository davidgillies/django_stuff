Usage:
> x = func('GP') # returns function from the dictionary for the GP model.


    def func(model):
       return {'volunteer': db.volunteers.all, 'GP': db.gps.all}[model]
