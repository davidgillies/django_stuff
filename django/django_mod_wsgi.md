1. Install apache, has to the right one to match your system, python version.
2. Install mod_wsgi, has to be the right one to match your system (e.g. 32, 64), python version and apache version.  You just drop the right mod_wsgi.so into the modules folder and address it correctly in the LoadModule statement below.
3. In your httpd.conf you have to define ServerRoot, DocumentRoot etc., comment out SSL stuff and calls httpd-sni.conf and httpd-ssl.conf as well as various config for these.
4. Add:

        LoadModule wsgi_module modules/mod_wsgi.so
    
        WSGIScriptAlias / U:/Data/show_case/study_manager/sm_project/sm_project/wsgi.py # 
        WSGIPythonPath U:/Data/show_case/study_manager/sm_project # python needs to find your project files
        WSGIPythonHome U:/Data/show_case/Scripts/python.exe # still doesn't work in a virtualenv this way though

        <Directory U:/Data/show_case/study_manager/sm_project/sm_project>
        <Files wsgi.py>
        Require all granted
        </Files>
        </Directory>
        
        
5. Obviously change your the apache settings above to match your django stuff.
6. Launch apache with the httpd.exe (probably just httpd in Mac)
7. Create a static files folder using **python manage collectstatic**.  This collects all your static crap into the STATIC_ROOT as defined in your settings e.g 

        STATIC_ROOT = 'U:/Data/show_case/study_manager/sm_project/static'

8. Next you have to set up an alias in httpd.conf:

        <Directory "U:/Data/show_case/study_manager/sm_project/static">
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Require local
        Require all granted
        </Directory>
        Alias /static U:/Data/show_case/study_manager/sm_project/static

Had to add all that guff to avoid getting a 403 Forbidden Error.

