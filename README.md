# django-docker
docker version of Django

# Install
Steps for setup:

$Step$ Create the Django project by running the docker-compose run command as follows.

Command: sudo docker-compose run web django-admin.py startproject composeexample .
 
 <<<<<<<<<<< Example output >>>>>>>>>>>
 
 [root@ubuntu /personal/isical/github/django-docker]# sudo docker-compose run web django-admin.py startproject composeexample .
 
Pulling db (postgres:)...
latest: Pulling from library/postgres
177e7ef0df69: Pull complete
……
Creating django-docker_db_1_9235f89f5f9f ... done
Building web
Step 1/7 : FROM python:3
3: Pulling from library/python
…..

 <<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>
 
 $Step$ Change the permission
 
 Command: sudo chown -R $USER:$USER .
 
 $$ list the content 
 
 <<<<<<<<<< Example output >>>>>>>>>>>>
 
 [root@ubuntu /personal/isical/github/django-docker]# ls -l
total 24
drwxr-xr-x 2 root root 4096 Jan  1 03:42 composeexample/
-rw-r--r-- 1 root root  211 Jan  1 03:34 docker-compose.yml
-rw-r--r-- 1 root root  144 Jan  1 03:34 Dockerfile
-rwxr-xr-x 1 root root  812 Jan  1 03:42 manage.py*
-rw-r--r-- 1 root root   41 Jan  1 03:33 README.md
-rw-r--r-- 1 root root   26 Jan  1 03:34 requirements.txt

 <<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
 
 $Step$ Connect the Database
 
 This example uses postgresql Database. You can view this in the composeexample/settings.py_new
 So, you need to replace settings.py
 
 Command:  cp composeexample/settings.py_new composeexample/settings.py
 
 
 <<<<<<<<<Example output >>>>>>>>>>>>>>>>>>
 
  [root@ubuntu /personal/isical/github/django-docker]# cat composeexample/settings.py | grep -A 10 DATABASE
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}

<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>
  
 $Step$ Run the docker-compose up command from the top level directory for your project.
 
Command:   docker-compose up
   
 <<<<<<<<<Example output>>>>>>>>>>>>>>>>>>>>>>>>>>
 
  djangosample_db_1 is up-to-date
Creating djangosample_web_1 ...
Creating djangosample_web_1 ... done
Attaching to djangosample_db_1, djangosample_web_1
db_1   | The files belonging to this database system will be owned by user "postgres".
db_1   | This user must also own the server process.
db_1   |
db_1   | The database cluster will be initialized with locale "en_US.utf8".
db_1   | The default database encoding has accordingly been set to "UTF8".
db_1   | The default text search configuration will be set to "english".

. . .

web_1  | May 30, 2017 - 21:44:49
web_1  | Django version 1.11.1, using settings 'composeexample.settings'
web_1  | Starting development server at http://0.0.0.0:8000/
web_1  | Quit the server with CONTROL-C.

<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

$Step$ Access the website and check if it works 

URL: http://localhost:8000 or http://<machine IP>:8000
 
 Where machine IP is the IP address of the machine on which django is installed.
  
You should see similar output as shown in the link https://docs.docker.com/compose/images/django-it-worked.png
 
 
# Cleanup 
$Cleanup$Stop the server

To stop the server, Use command Ctrl+c 

It will gracefully stop the server

To immediately kill the server, again press Ctrl+c

To clean the data, just remove the folder using rm -rf command

# Reference
https://docs.docker.com/compose/django/#connect-the-database
