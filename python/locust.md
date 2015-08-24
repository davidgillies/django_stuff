Install locust

    pip install locustio
    
Create a local locustfile.py

    from locust import HttpLocust, TaskSet



    def login(l):
        l.client.get("/admin/login/?next=/admin/", auth=("admin", "admin"))

    def index(l):
        l.client.get("/admin/api_renderer/volunteer/")

    def profile(l):
        l.client.get("/admin/api_renderer/surgery/")

    class UserBehavior(TaskSet):
        tasks = {index:2, profile:1}

        def on_start(self):
            """ Run on start for every Locust hatched """
            r = self.client.get('/admin/login/?next=/admin/')
            self.client.post('/admin/login/?next=/admin/', 
                {'username': 'admin', 'password': 'admin',
                 'csrfmiddlewaretoken': r.cookies['csrftoken']})

    class WebsiteUser(HttpLocust):
        task_set = UserBehavior
        min_wait=5000
        max_wait=9000


To run the locust server:

    locust -f U:\wherever\locustfile.py --host=http://localhost:9000
