# BoilerPlateCode_Django_Python

Django - Project (Twitter) - 


1. Create Folder Python-Django-Project-Twitter.
2. Terminal -> Create new virtual environment -> python3 -m venv .venv
3. Terminal -> Activate virtual environment -> source .venv/bin/activate
4. Terminal -> Install Django -> pip install django
5. Terminal -> Upgrade pip -> pip install --upgrade pip
6. Terminal -> Freeze pip versions -> pip freeze > requirements.txt
7. Terminal -> Create project -> django-admin startproject djangotwitter
8. Terminal -> Go inside folder -> cd djangotwitter
9. Terminal -> Check for manage.py file -> ls
10. Terminal -> Run Server -> python manage.py runserver
11. Browser -> http://127.0.0.1:8000/
12. Terminal -> Remover Error while running server first time step -> CONTROL-C
    1. Terminal -> python manage.py makemigrations
    2. Terminal -> python manage.py migrate
    3. Terminal -> python manage.py runserver
13. Terminal -> Admin create super user -> CONTROL-C
    1. Terminal -> python manage.py createsuperuser
    2. Terminal -> Enter name -> prince
    3. Terminal -> Enter email -> princeatwar.k@gmail.com 
    4. Terminal -> Enter Password -> Tabaraki@1299
    5. Terminal -> Confirm Password -> Tabaraki@1299
    6. Terminal -> python manage.py runserver
    7. Browser -> http://127.0.0.1:8000/admin
    8. Browser -> Enter admin name & password
14. Configure Media in settings.py file -> Root Folder -> settings.py ->  import os
    1. Root Folder -> settings.py ->  write below DEFAULT_AUTO_FIELD -> MEDIA_URL = '/media/'
    2. Root Folder -> settings.py ->  write below MEDIA_URL -> MEDIA_ROOT = os.path.join(BASE_DIR, 'media') 
15. Configure Static in settings.py -> Root Folder -> settings.py -> write below STATIC_URL ->  STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')] 
    1. Root Folder -> create new static folder
    2. Root Folder -> urls.py -> urlpatterns[…] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
    3. Root Folder -> urls.py -> from django.conf import settings
    4. Root Folder -> urls.py -> from django.conf.urls.static import static
16. Create New Apps in Django Project -> Terminal -> CONTROL-C
    1. Terminal -> python manage.py startapp tweet
    2. tweet app folder -> create new urls.py file
        1. tweet app folder -> urls.py -> copy and paste whole file from root folder urls.py file except ‘+ static part and static imports’
17. Create New View in app -> tweet app folder -> views.py -> def index(request): return render(request, 'index.html')
    1. tweet app folder -> urls.py -> from . import views
    2. tweet app folder -> urls.py -> from django.urls import path
    3. tweet app folder -> urls.py -> urlpatterns array -> path('', views.index, name='index'),
    4. Root Folder -> settings.py -> INSTALLED_APP array -> 'tweet',
    5. Root Folder -> settings.py -> TEMPLATES array -> 'DIRS': [os.path.join(BASE_DIR, 'templates')],
    6. tweet folder -> create new templates folder 
        1. tweet folder -> templates folder -> create new index.html file
        2. tweet folder -> templates folder -> index.html -> ! And hit enter
        3. tweet folder -> templates folder -> index.html -> <body> test template </body>
    7. Root Folder -> urls.py -> urlpatterns array -> from django.urls import path, include
    8. Root Folder -> urls.py -> urlpatterns array -> path('tweet/', include('tweet.urls')),
    9. Terminal (Quit Run Server if running) -> python manage.py runserver
    10. Browser -> http://127.0.0.1:8000/tweet
18. Create Home Page in Root folder -> djangotwitter folder -> create new file views.py
    1. Root folder -> create new templates folder -> create another new home folder
        1. Root folder -> templates folder -> home folder -> create new index.html file
        2. Root folder -> templates folder -> home folder -> index.html -> ! And hit enter
        3. Root folder -> templates folder -> home folder -> index.html -> <body> Home Page </body>
    2. djangotwitter folder -> views.py -> from django.shortcuts import render def home(request): return render(request, 'home/index.html')
    3. djangotwitter folder -> urls.py -> from . import views
    4. djangotwitterfolder -> urls.py -> from django.urls import path
    5. djangotwitter folder -> urls.py -> urlpatterns array -> path('', views.home, name=‘home’),
    6. Terminal (Quit Run Server if running) -> python manage.py runserver
    7. Browser -> http://127.0.0.1:8000/
19. Create base layout theme for the project -> Root Templates folder -> create new layout.html file 
    1. root templates folder -> layout.html file -> {% load static %}
    2. root templates folder -> layout.html file -> ! and hit enter
    3. root templates folder -> layout.html file -> <title> -> block unnamed and hit enter
    4. root templates folder -> layout.html file -> <title> {% block title %} Django Twitter {% endblock %} </title>
    5. root templates folder -> layout.html file -> <body> -> div.container and hit enter
    6. root templates folder -> layout.html file -> <body> -> block unnamed and hit enter
    7. root templates folder -> layout.html file -> <body> <div class="container"> {% block content %}{% endblock %} </div> </body>
20. Load Bootstrap for css in the project -> Browser -> https://getbootstrap.com/docs/5.3/getting-started/introduction/
    1. Copy and paste in layout.html file -> <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    2. Use Bootstrap in tweet app -> tweet folder -> templates folder -> index.html file -> clear the whole file 
        1. tweet folder -> templates folder -> index.html file -> extends and hit enter
        2. tweet folder -> templates folder -> index.html file -> {% extends "layout.html" %}
        3. tweet folder -> templates folder -> index.html file -> block unnamed and hit enter
        4. tweet folder -> templates folder -> index.html file -> {% block title %} Django Twitter {% endblock %}
        5. tweet folder -> templates folder -> index.html file -> block unnamed and hit enter
        6. tweet folder -> templates folder -> index.html file -> {% block content %} <h1 class="text-center mt-4”>Welcome to Django Twitter Project</h1> {% endblock %}
        7. root templates folder -> layout.html file -> <html lang="en" data-bs-theme="dark">
    3. Create nav bar for tweet app -> Browser -> https://getbootstrap.com/docs/5.3/getting-started/introduction/
        1. Search for nav bar and copy and paste it to root folder layout.html file above content block
21. Create models in tweet app -> tweet app folder -> models.py file -> from django.contrib.auth.models import User 
    1. tweet app folder -> models.py file -> create class of Tweet
    2. tweet app folder -> models.py file -> 
        1. class Tweet(models.Model):
        2. user = models.ForeignKey(User, on_delete=models.CASCADE)
        3. text = models.TextField(max_length=240)
        4. photo = models.ImageField(upload_to='photos/', blank=True, null=True)
        5. created_at = models.DateTimeField(auto_now_add=True)
        6. updated_at = models.DateTimeField(auto_now=True)
        7. def __str__(self):
        8. return f'{self.user.username} - {self.text[:10]}'
    3. Install pillow for ImageField -> Terminal (Quit Run Server if running)-> python -m pip install Pillow
    4. Terminal -> cd ..
    5. Terminal -> pip freeze > requirements.txt
    6. Terminal -> cd djangotwitter
    7. Terminal -> python manage.py makemigrations tweet
    8. Terminal -> python manage.py migrate
    9. Terminal -> python manage.py runserver 
    10. Register Tweet Model to admin -> tweet app folder -> admin.py file -> from .models import Tweet
        1. tweet app folder -> admin.py file -> admin.site.register(Tweet)
        2. Browser -> http://127.0.0.1:8000/admin/
        3. Browser -> http://127.0.0.1:8000/admin/ -> Add new Tweet on admin panel
22. Create forms in tweet app -> tweet app folder -> create new file forms.py
    1. tweet app folder -> forms.py -> from django import forms
    2. tweet app folder -> forms.py -> from .models import Tweet
    3. tweet app folder -> forms.py -> create class TweetForm ->
        1. class TweetForm(forms.ModelForm):
        2. class Meta:
        3. model = Tweet
        4. fields = ['text', 'photo']
23. Create some views in tweet app -> tweet app folder -> views.py ->
    1. tweet app folder -> views.py -> from .models import Tweet
    2. tweet app folder -> views.py -> from .forms import TweetForm
    3. tweet app folder -> views.py -> from django.shortcuts import get_object_or_404, redirect
    4. tweet app folder -> views.py -> Create new def tweet_list ->
        1. def tweet_list(request):
        2. tweets = Tweet.objects.all().order_by('-created_at')
        3. return render(request, 'tweet_list.html', {'tweets' : tweets})
    5. tweet app folder -> views.py -> Create new def tweet_create ->
        1. def tweet_create(request):
        2. if request.method == 'POST':
        3. form = TweetForm(request.POST, request.FILES)
        4. if form.is_valid():
        5. tweet = form.save(commit=False)
        6. tweet.user = request.user
        7. tweet.save()
        8. return redirect('tweet_list')
        9. else:
        10. # In case form is not valid, re-render with errors
        11. return render(request, 'tweet_form.html', {'form': form})
        12. else:
        13. form = TweetForm()
        14. return render(request, 'tweet_form.html', {'form' : form})
    6. tweet app folder -> views.py -> Create new def tweet_edit ->
        1. def tweet_edit(request, tweet_id):
        2. tweet = get_object_or_404(Tweet, pk=tweet_id, user = request.user)
        3. if request.method == 'POST':
        4. form = TweetForm(request.POST, request.FILES, instance=tweet)
        5. if form.is_valid():
        6. tweet = form.save(commit=False)
        7. tweet.user = request.user
        8. tweet.save()
        9. return redirect('tweet_list')
        10. else:
        11. form = TweetForm(instance=tweet)
        12. return render(request, 'tweet_form.html', {'form' : form})
    7. tweet app folder -> views.py -> Create new def tweet_delete ->
        1. def tweet_delete(request, tweet_id):
        2. tweet = get_object_or_404(Tweet, pk=tweet_id, user = request.user)
        3. if request.method == 'POST':
        4. tweet.delete()
        5. return redirect('tweet_list')
        6. return render(request, 'tweet_confirm_delete.html', {'tweet' : tweet})
24. Create Jinja Templates for tweet app -> tweet app folder -> templates folder -> 
    1. tweet app folder -> templates folder -> create new file tweet_list.html -> 
        1. {{% extends "layout.html" %}
        2. {% block title %}
        3. Django Twitter
        4. {% endblock %}
        5. {% block content %}
        6. <h1 class="text-center mt-4">Tweet List</h1>
        7. <a class="btn btn-primary mb-4” href="{% url 'tweet_create' %}">Create a Tweet</a>
        8. <div class="container row gap-3">
        9. {% for tweet in tweets %}
        10. <div class="card" style="width: 18rem;">
        11. <img src="{{tweet.photo.url}}" class="card-img-top" alt="...">
        12. <div class="card-body">
        13. <h5 class="card-title">{{tweet.user.username}}</h5>
        14. <p class="card-text">{{tweet.text}}</p>
        15. {% if tweet.user == user %}
        16. <a href="{% url 'tweet_edit' tweet.id %}" class="btn btn-primary">Edit</a>
        17. <a href="{% url 'tweet_delete' tweet.id %}" class="btn btn-danger">Delete</a>
        18. {% endif %}
        19. </div>
        20. </div>
        21. {% endfor %}
        22. </div>
        23. {% endblock %}
    2. tweet app folder -> templates folder -> create new file tweet_form.html -> 
        1. {% extends "layout.html" %}
        2. {% block title %}
        3. Django Twitter
        4. {% endblock %}
        5. {% block content %}
        6. <h1 class="text-center mt-4">Tweets</h1>
        7. <h2>{% if form.instance.pk %} Edit Tweet {% else %} New Tweet {% endif %}</h2>
        8. <form method="post" enctype="multipart/form-data" class="form">
        9. {% csrf_token %}
        10. {{ form.as_p }}
        11. {% if form.errors %}
        12. <ul class="errors">
        13. {% for field in form %}
        14. {% for error in field.errors %}
        15. <li>{{ error }}</li>
        16. {% endfor %}{% endfor %}
        17. </ul>
        18. {% endif %}
        19. <button class="btn btn-warning" type="submit">Submit</button></form>
        20. <a href="{% url 'tweet_list' %}">Back</a>
        21. {% endblock %}
    3. tweet app folder -> templates folder -> create new file tweet_confirm_delete.html -> 
    4. {% extends "layout.html" %}
    5. {% block title %}
    6. Django Twitter
    7. {% endblock %}
    8. {% block content %}
    9. <h1 class="text-center mt-4">Tweets</h1>
    10. <h2>Are you sure that you want to delete the tweet?</h2>
    11. <form method="post">
    12. {% csrf_token %}
    13. <button class="btn btn-danger">Delete</button>
    14. <a class="btn btn-success" href="{% url 'tweet_list' %}">Cancel</a>
    15. </form>
    16. {% endblock %}
25. Configure urls for Jinja templates -> tweet app folder -> urls.py file ->
    1. tweet app folder -> urls.py file -> urlspatterns array ->
        1. urlpatterns = [
        2. # path('', views.index, name='index'),
        3. path('/home', views.index, name='index'),
        4. path('', views.tweet_list, name='tweet_list'),
        5. path('create/', views.tweet_create, name='tweet_create'),
        6. path('<int:tweet_id>/edit/', views.tweet_edit, name='tweet_edit'),
        7. path('<int:tweet_id>/delete/', views.tweet_delete, name='tweet_delete'),
        8. ]
26. Browser (must login in /admin to use tweet app) -> http://127.0.0.1:8000/tweet/
27. Create protected routes (User must be logged in to use the app)-> tweet app folder -> views.py file -> from django.contrib.auth.decorators import login_required 
    1. tweet app folder -> views.py file -> add decorator above tweet_create def -> @login_required
    2. tweet app folder -> views.py file -> add decorator above tweet_edit def -> @login_required
    3. tweet app folder -> views.py file -> add decorator above tweet_delete def -> @login_required
    4. Browser -> Turn on Incognito Mode -> http://127.0.0.1:8000/tweet/create/
28. Create User Registration Form -> tweet app folder -> forms.py file -> from django.contrib.auth.forms import UserCreationForm 
    1. tweet app folder -> forms.py file -> from django.contrib.auth.models import User
    2. tweet app folder -> forms.py file -> 
        1. class UserRegistrationForm(UserCreationForm):
        2. email = forms.EmailField()
        3. class Meta:
        4. model = User
        5. fields = ('username', 'email', 'password1', 'password2')
29. Create User Registration Jinja Templates -> root folder -> templates folder -> create new folder registration
    1. root folder -> templates folder -> registration folder -> create new file register.html -> 
        1. {% extends "layout.html" %}
        2. {% block title %} Django Twitter - Register {% endblock %}
        3. {% block content %}
        4. <h2>Register</h2>
        5. <form method="post">
        6. {% csrf_token %}
        7. {{form.as_p}}
        8. <button class="btn btn-primary">Register</button>
        9. </form>
        10. <p>Already have an account? <a href="{% url 'login' %}">Login</a></p>
        11. {% endblock %}
    2. root folder -> templates folder -> registration folder -> create new file login.html ->
        1. {% extends "layout.html" %}
        2. {% block title %} Django Twitter - Login {% endblock %}
        3. {% block content %}
        4. <h2>Login</h2>
        5. <form method="post">
        6. {% csrf_token %}
        7. {{form.as_p}}
        8. <button class="btn btn-primary">Login</button>
        9. </form>
        10. <p>Don't have an account? <a href="{% url 'register' %}">Register</a></p>
        11. {% endblock %}
    3. root folder -> templates folder -> registration folder -> create new file logged_out.html -> 
        1. {% extends "layout.html" %}
        2. {% block title %} Django Twitter {% endblock %}
        3. {% block content %}
        4. <h2>Logged Out</h2>
        5. <p>You have been logged out <a href="{% url 'login' %}">Login Again</a></p>
        6. {% endblock %}
30. Create User Registration Views -> tweet app folder -> views.py file -> from .forms import TweetForm , UserRegistrationForm
    1. tweet app folder -> views.py file -> from django.contrib.auth import login
        1. tweet app folder -> views.py file ->  def register(request):
        2. if request.method == 'POST':
        3. form = UserRegistrationForm(request.POST)
        4. if form.is_valid():
        5. user = form.save(commit=False)
        6. user.set_password(form.cleaned_data['password1'])
        7. user.save()
        8. login(request, user)
        9. return redirect('tweet_list')
        10. else:
        11. form  = UserRegistrationForm()
        12. return render(request,'registration/register.html', {'form' : form})
    2. tweet app folder -> urls.py file -> urlpatterns array -> path('register/', views.register, name='register'),
    3. Root djangotwitter folder -> settings.py file -> 
        1. LOGIN_URL = '/accounts/login'
        2. LOGIN_REDIRECT_URL = '/tweet/' 
        3. LOGOUT_REDIRECT_URL = '/tweet/'
    4. Root djangotwitter folder -> urls file -> from django.contrib.auth.urls import views as auth_views
        1. Root djangotwitter folder -> urls file -> urlpatterns array -> path('accounts/', include('django.contrib.auth.urls')),
31. Add Logout Button to Navbar -> root djangotwitter folder -> templates folder -> layout.html file -> add below search form -> 
    1. <a href="{% url 'tweet_list' %}" class="btn btn-primary mx-2">Home</a>
    2. {% if user.is_authenticated %}
    3. <form action="{% url 'logout' %}" method="post">
    4. {% csrf_token %}
    5. <button class="btn btn-danger" type="submit">Logout</button>
    6. </form>
    7. {% else %}
    8. <a href="{% url 'register' %}" class="btn btn-primary mx-2">Register</a>
    9. <a href="{% url 'login' %}" class="btn btn-success mx-2">Login</a>
    10. {% endif %}
32. Browser (Incognito Mode) Try Login & Logout -> http://127.0.0.1:8000/tweet/
33. Deploy in Vercel -> Terminal -> python manage.py collectstatic
    1. root djangotwitter folder -> settings.py file -> ALLOWED_HOSTS = [‘*’]
    2. Terminal -> python -m pip install gunicorn
    3. Terminal -> pip freeze > requirements.txt
    4. Terminal -> python -m pip install whitenoise
    5. Terminal -> pip freeze > requirements.txt
    6. root djangotwitter folder -> wsgi.py file -> app = application
    7. root djangotwitter folder -> settings.py file -> STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles’)
    8. root djangotwitter folder -> settings.py file -> MIDDLEWARE array ->  'whitenoise.middleware.WhiteNoiseMiddleware',
    9. root djangotwitter folder -> settings.py file -> INSTALLED_APPS array -> 'whitenoise.runserver_nostatic',
    10. root directory -> create vercel.json file (may work or try version 2 or 3) ->
        1. {
        2. "version": 2,
        3. "builds": [
        4. {
        5. "src": "manage.py",
        6. "use": "@vercel/python",
        7. "config": {
        8. "maxDuration": 10
        9. }
        10. }
        11. ],
        12. "routes": [
        13. {
        14. "src": "/(.*)",
        15. "dest": "/manage.py"
        16. }
        17. ]
        18. }
    11. root directory -> create vercel.json file (version 2) ->
        1. {
        2. "version" : 2,
        3. "builds" : [
        4. {
        5. "src" : "djangotwitter/wsgi.py",
        6. "use" : "@vercel/python",
        7. "config" : { "maxLamdaSize" : "15mb", "runtime" : "python3.”9 }
        8. },
        9. {
        10. "src" : "build_files.sh",
        11. "use" : "@vercel/static-build",
        12. "config" : { "distDir" : "staticfiles_build" }
        13. }
        14. ],
        15. "routes" : [
        16. {
        17. "src" : "/stactic/(.*)",
        18. "dest" : "/static/$1"
        19. },
        20. {
        21. "src" : "/(.*)",
        22. "dest" : "djangotwitter/wsgi.py"  
        23. }
        24. ]
        25. }
    12. root directory -> create vercel.json file (version 3) ->
        1. {
        2. "builds": [
        3. {
        4. "src": "djangotwitter/wsgi.py",
        5. "use": "@vercel/python",
        6. "config" :{ "maxLambdaSize" : "15mb", "runtime" : "python3.11.3" }
        7. }
        8. ],
        9. "routes": [
        10. {
        11. "src": "/(.*)",
        12. "dest": "djangotwitter/wsgi.py"
        13. }
        14. ]
        15. }
    13. root directory -> create build_files.sh file ->
        1. echo "BUILD START"
        2. python3.9 -m pip install -r requirements.txt
        3. python3.9 manage.py collectstatic --noinput --clear
        4. echo "BUILD END"
34. 











