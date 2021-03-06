## INSTALL DEPENDENCIES

easy_install simplejson
easy_install anyjson
easy_install celery
easy_install sqlalchemy # for celery to store data
sudo port install rabbitmq-server


## HOWTO RUN

- install and start web2py
- install this app
- run the app once (it will built the tables)
- cd applications/<app>/modules/plugin_celery
- run concurrently:
``
 sudo rabbitmq-server -detached 
 export WEB2PY_PATH=/path/to/web2py
 celeryd --loglevel=DEBUG -E
 celerybeat -S scheduler.Web2pyScheduler --loglevel=DEBUG
 celeryev -c camera.Web2pyCamera --frequency=2.0
 celeryev
``
 (notice all these processes may run on different machines but celerybeat and celeryev
  will need access to the databases/ folder).
- now visit http://127.0.0.1:8000/<app>/plugin_celery
- use the menu
- submit a non periodic task with 
  http://127.0.0.1:8000/<app>/plugin_celery/create_task
- periodic tasks are created via (does ot work yet)
  http://127.0.0.1:8000/<app>/plugin_celery/edit_periodictask
- create new tasks by editing modules/plugin_celery/tasks.py
- edit modules/plugin_celery/celeryconfig.py if needed

## LICENSE

New BSD License

## ACKNOWLEGEMENTS

This project is a rewrite but heavily based on django-celery.
We thank Ask Solem, developer of celery and django-celery for his work and his help.

This project was supported by Sahana Eden

## USEFUL REFERENCES

- http://mathematism.com/2010/02/16/message-queues-django-and-celery-quick-start/
- http://packages.python.org/django-celery/introduction.html
