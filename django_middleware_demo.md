Django middleware works on either the request or the response.  They are reigstered in order in the settings.py of your project e.g.

    MIDDLEWARE_CLASSES = (
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.auth.middleware.SessionAuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
        'html_renderer.middleware.BeautifulMiddleware',
    )
    
This lot work in order, going down the list when dealing with the request and going back up when dealing with the response.  Here I have added a class at the bottom.  In this case I put middleware.py in my html_renderer app with the class BeautifulMiddleware in it.  The class looks like this:

    from bs4 import BeautifulSoup

    class BeautifulMiddleware(object):
        def process_response(self, request, response):
            if response.status_code == 200:
                if response["content-type"].startswith("text/html"):
                    beauty = BeautifulSoup(response.content)
                    response.content = beauty.prettify()
            return response

This uses the process_response() hook.  There are a number of hooks available:
https://docs.djangoproject.com/en/1.7/topics/http/middleware/
