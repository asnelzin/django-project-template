## {{ project_name|title }} for development

First of all, you should have the following tools installed on your machine:

    - python >= 2.7
    - pip <http://www.pip-installer.org/> >= 1.5
    - virtualenv <http://www.virtualenv.org/> >= 1.10
    - virtualenvwrapper <http://pypi.python.org/pypi/virtualenvwrapper> >= 3.0
    - Postgres >= 9.1
    - git >= 1.7


### Getting started

First clone the repository from Github and switch to the new directory:
    
    git clone https://github.com/asnelzin/{{ project_name }}.git
    cd {{ project_name }}

To setup your local environment you should create a virtualenv and install the
necessary requirements::

    mkvirtualenv {{ project_name }}
    $VIRTUAL_ENV/bin/pip install -r $PWD/requirements/dev.txt

Then create a local settings file and set your ``DJANGO_SETTINGS_MODULE`` to use it:

    cp {{ project_name }}/settings/local.example.py {{ project_name }}/settings/local.py
    echo "export DJANGO_SETTINGS_MODULE={{ project_name }}.settings.local" >> $VIRTUAL_ENV/bin/postactivate
    echo "unset DJANGO_SETTINGS_MODULE" >> $VIRTUAL_ENV/bin/postdeactivate

Exit the virtualenv and reactivate it to activate the settings just changed:

    deactivate
    workon {{ project_name }}

Create the Postgres database and run the initial syncdb/migrate:

    createdb -E UTF-8 {{ project_name }}
    python manage.py syncdb
    python manage.py migrate

You should now be able to run the development server:

    python manage.py runserver