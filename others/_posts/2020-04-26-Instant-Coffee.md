---
image:
  teaser: others.jpg

layout: article
title: Love Hurricane Among Django, Front-end and Heroku
date: 2020-04-27
categories: notes
author: chunyi_hsiao
tags: [Python, Django, Heroku]
share: true
---

<h4>Nella said "Love is complated, and hurricane is scary."</h4>
How it works when they are involved in a love hurricane with django, front-end and heroku?



* goal to go: build [my online resume](https://hsiaocy.herokuapp.com/)
* things to have: 
	1. Django - overall web framework
	2. front-end - [a fancy template](https://freehtml5.co/profile-free-html5-bootstrap-template-for-personal-and-vcard-resume-websites/)
	3. heroku - deploy your site

Story:  
1. Django
	- **prerequisites**: python3.x, venv and Django pack are already installed
	- **Create a project**: it contains all the stuff we will mention later, here use "UnchainedDjango" as my project name. Oepn CLI and change directory to "UnchainedDjango/" to create project. Keeping use UnchainedDjango as project name, and you will get a tree like
	<pre class="brush: bash">
		django-admin startproject UnchainedDjango
		cd UnchainedDjango

		.(UnchainedDjango)  <- root dir, "git init" here for heroku deployment
		├── manage.py       <- our tool script (python3 manage.py [func])
		└── unchaineddjango <- (project manager?)
		    ├── __init__.py
		    ├── asgi.py
		    ├── settings.py <- site configuratin manager
		    ├── urls.py     <- url's boss which manages all sites, import app's site here
		    └── wsgi.py
	</pre>
	- **Create a app**: to generate a folder which points to the site(app). If you want to modify at site, modify here. More detail: [link](https://docs.djangoproject.com/en/3.0/intro/tutorial01/#creating-the-polls-app)

	<pre class="brush: bash">
		django-admin startapp homepage

		.(UnchainedDjango)  <- root dir, "git init" here for heroku deployment
		├── manage.py
		├── unchaineddjango/
		└── hoamepage/
			├── migrations/
			│	└─__init__.py
		    ├── __init__.py
		    ├── admin.py
		    ├── app.py
		    ├── models.py
		    ├── tests.py
		    ├── urls.py     <- not default created, need to create by myself
		    └── views.py   
	</pre>

	- **Set app into config(setting.py)**:
		- open file **UnchainedDjango/setting.py** when **testing**... 
			- add app path ```INSTALLED_APPS[ ..., 'homepage',]```
			- add template path ```'DIRS': [os.path.join(BASE_DIR, 'templates').replace('\\', '/')],```  
			- add static path ```STATIC_ROOT = os.path.abspath(os.path.join(BASE_DIR, 'static'))```
			- add static-files path ```STATICFILES_DIRS = [os.path.join(BASE_DIR, "static"), '/var/www/static/',]```
			- make sure "DEBUG=True"  
		- open file **UnchainedDjango/setting.py** when **deploy**... 
			- add static path ```STATIC_ROOT = 'static'```
			- add HTTP connection ```SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')'```
			- add to allow all domain to reach```ALLOWED_HOSTS = ['*']```


	- **Summary**:

		- Since a bunch of tutorials can guide you to do so, I dont't explain everything detailedly.
		- Some frequently obstruction orrcurred:
			- nope
		- Frequently opened files:
			- ./UnchainedDjango/setting.py: config manager
			- ./UnchainedDjango/urls.py: url manager
			- ./homepage/urls.py: 
			- ./homepage/views.py: 
			- ./template/homepage.html: the site/app write in html
			- ./static/homepage/* : is created by myself and may contain: css, fonts, images, js and sass
			<pre class="brush: bash">
				django-admin startapp homepage

				.(static)       <- based on root dir, all site structure are placed here
				└── hoamepage/  <- create folder for your app
					├── css/
					│	├─ style.css
					│	└─ ...
				    ├── fonts/
					│	├─ icomoon/
					│	└─ ...
				    ├── images/
					│	└─ you_are_fㄩㄈking_handsome.jpg
				    ├── js/
					│	├─ main.js
					│	└─ ...
				    └── sass/
					 	└─ ...
			</pre>

2. Front-end
	- Basically, when we download [a fancy template](https://freehtml5.co/profile-free-html5-bootstrap-template-for-personal-and-vcard-resume-websites/), that will contain a ```.html``` file (may be named ```index.html```, ```home.html```, ```page.html``` whatever, I will use homepage.html here) which is the page file going to show on your app. 
	- Need to do is populating the whole pack into our Django environment
		- create ```static/``` and ```template/``` folders under root path(UnchainedDjango)
			- create ```homepage/``` under ```static/``` and place template package here
			- place my ```homepage.html``` file at ```template/```
		

		- add a tag in the ```homepage.html``` to load and refer ```static/```
		- change all the src path in tag and correct to ```static/```
		- It's cumbersome and time-spent to change all path and src, so literally troubleshoot it from the error messages...

	- Add in UnchiainedDjango/urls.py
		- import html file:  
			```from homepage.views import homepage```   
			```urlpatterns = [ ..., url(r'^$', homepage),]```  

	Preference: [**Managing static files (e.g. images, JavaScript, CSS)**](https://docs.djangoproject.com/en/3.0/howto/static-files/)  


3. Heroku deploy
	- **prerequisites**:
		- knowladge of Git version control
		- Heroku [**sign-up**](https://signup.heroku.com) and [**install**](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)
		- install packages: ```pip3 install dj-database-url dj-static gunicorn psycopg2```
		- from test to prod: ```DEBUG=False```
		- create three files:
			- **Procfile**
				- just create the file named Procfile without any extension
				- open Procfile and insert following command:
					<pre class="brush: bash">web: gunicorn --pythonpath mysite mysite.wsgi --log-file - </pre>
			- **runtime.txt**
				- insert your python version, e.g. mine is 3.6.5
					<pre class="brush: bash">python-3.6.5</pre>
			- **requirements.txt**
				- type at root dir
					<pre class="brush: bash"> pip3 freeze > requirements.txt</pre>

				- then open "requirements.txt" and insert this package in the file  
					<pre class="brush: bash">psycopg2</pre>
		- modify wsgi.py
			<pre class="python">
				import os
				from django.core.wsgi import get_wsgi_application
				from dj_static import Cling
				os.environ.setdefault("DJANGO_SETTINGS_MODULE", "UnchainedDjango.settings")
				application = Cling(get_wsgi_application())
			</pre>
	- **Creat Heroku remote**:
		- ```git init```: **heroku use git**, thus git control is needed for this project
		- ```heroku login```: login your account
		- ```heroku create your_app_name```: create a new heroku app
			- for example: ```heroku create UnchainedDjango```
			- Otherwise, ```heroku create``` will automatically assign a app-name for you like ```Glacier-Grag-12345```
			- But, ```git remote rename heroku another-name``` can rename your app
		- ```git remote -v```: confirm the remote has been set
		- ```git push heroku master```: deploy code

	Preference: [**Deploying with Git**](https://devcenter.heroku.com/categories/deploying-with-git)  
	
***update date: 2020-04-28***

