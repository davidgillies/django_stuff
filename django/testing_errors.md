## Testing Errors
On Windows when trying to run the tests with
    python manage.py test
    
it gave errno 10013 regarding access permissions to sockets.  To get it to work use

    python manage.py test --liveserver=localhost:8082
    
Another thing was when I restructured things I had a tests.py module and a tests folder where I rearranged the tests.  So if you get any import issues, you need to bin the old file.
