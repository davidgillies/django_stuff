Simple example, sqlsoup reads the table structures and uses sqlalchemy to give you an ORM:
  
  
    import sqlsoup
    db = sqlsoup.SQLSoup('mysql+pymysql://david:david@localhost:3306/sm_play')
    volunteers = db.volunteers.all()
    for v in volunteers:
        print v.id, v.surname