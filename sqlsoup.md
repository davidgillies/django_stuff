Simple example, sqlsoup reads the table structures and uses sqlalchemy to give you an ORM:
  
  
    import sqlsoup
    db = sqlsoup.SQLSoup('mysql+pymysql://david:david@localhost:3306/sm_play')
    volunteers = db.volunteers.all()
    for v in volunteers:
        print v.id, v.surname
    
    db.table = db.entity('some_table_name') # get a table from a string.
    db.table.get(2) # get from table by primary key
    data = db.table.get(2).__dict__ # returns a dictionary of the record.
    data.pop('_sa_instance_state') # pops the instance object from your dictionary.
    db.table.filter_by(id=5).update(some_dict) # an update by sending a dictionary.
    db.table.insert(**some_dict) # inserts a dictionary.
    instance = db.table.get(5) 
    db.table.delete(instance) # delete an instance.  WARNING: cocking it up can delete the whole table.  
    db.commit() # commit changes.
    
    
