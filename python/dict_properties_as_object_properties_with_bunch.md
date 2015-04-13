      from bunch import Bunch
      
      
      class SomeClass():
        def __init__(self):
            self.thing = Bunch({'all': self.all, 'get': self.get,
                              'create': self.create,
                              'update': self.update, 'delete': self.delete})
      
      s = SomeClass()
      s.thing.all() # runs all function.
      
      # Alternatively
      mydict = {'all': all, 'get': get,
                'create': create,
                'update': update, 'delete': delete}
      
      obj = Bunch(mydict)
      
      # now can do this:
      obj.all() # to run the all function on whatever object you were in.
      
