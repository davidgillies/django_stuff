## Testing Errors
On Windows when trying to run the tests with
    python manage.py test
    
it gave errno 10013 regarding access permissions to sockets.  To get it to work use

    python manage.py test --liveserver=localhost:8082
    
