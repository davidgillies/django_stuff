    r=db.execute('''SELECT name FROM sqlite_master WHERE type='table';''')
    r.fetchall()
