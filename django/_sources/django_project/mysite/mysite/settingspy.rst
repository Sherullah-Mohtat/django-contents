settings.py
=============

-------------------------
1. What is settings.py?
-------------------------

The settings.py file contains all global configuration for a Django project, including installed apps, database settings, middleware, security options, and localization preferences.

settings.py is the central configuration file of a Django project.

Location:

.. code-block:: bash 

    mysite/mysite/settings.py

This file controls **how your entire Django project behaves.**

If Django is a machine, settings.py is its **control panel.**

=================================================================================================

------------------------------------
2. What does settings.py control?
------------------------------------

settings.py defines:
	- Installed apps
	- Database configuration
	- Middleware
	- Security options
	- Templates
	- Static & media files
	- Time zone & language
	- Debug mode

Django **cannot start** without this file.

=================================================================================================

---------------------------------
3. How Django uses settings.py
---------------------------------

When you run:

.. code-block::  bash 

    python manage.py runserver

Django:
	1.	Loads mysite.settings
	2.	Reads every configuration value
	3.	Initializes the project using those values

That’s why manage.py, asgi.py, and wsgi.py all reference:

.. code-block:: python 

    DJANGO_SETTINGS_MODULE = "mysite.settings"

=================================================================================================

1️⃣ Project base settings
--------------------------

.. code-block:: python 

    from pathlib import Path

    BASE_DIR = Path(__file__).resolve().parent.parent

- ASE_DIR points to the project root
- Used for paths like database, static files, templates


2️⃣ Security & debug
---------------------

.. code-block:: python 

    SECRET_KEY = 'django-insecure-...'
    DEBUG = True
    ALLOWED_HOSTS = []

Explanation:
	- SECRET_KEY → cryptographic security key
	- DEBUG=True → show detailed errors (dev only)
	- ALLOWED_HOSTS → domains allowed to access the site

⚠️ In production:

.. code-block:: python 

    DEBUG = False

3️⃣ Installed applications
---------------------------

.. code-block:: python 

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',

        'myapp',
    ]

This tells Django:
	- Which apps are enabled
	- Which features are active

Your app **must be listed here** to work.

4️⃣ Middleware
----------------

.. code-block:: python 

    MIDDLEWARE = [
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]

Middleware:
	- Runs **before & after every request**
	- Handles security, sessions, authentication, etc.

5️⃣ URL configuration
-----------------------

.. code-block:: python 

    ROOT_URLCONF = 'mysite.urls'

This tells Django:
    “Use urls.py to route incoming requests.”

6️⃣ Templates
--------------

.. code-block:: python 

    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [],
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]

Controls:
	- HTML rendering
	- Template locations
	- Context variables

7️⃣ Database configuration
---------------------------

.. code-block:: python 

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
        }
    }

Default:
	- SQLite database
	- Stored in db.sqlite3

Later, you can replace this with PostgreSQL or MySQL.

8️⃣ Password validation
------------------------

.. code-block:: python 

    AUTH_PASSWORD_VALIDATORS = [
        {'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator'},
        {'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator'},
        {'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator'},
        {'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator'},
    ]

Used by:
	- Admin panel
	- User authentication

9️⃣ Language & time zone
-------------------------

.. code-block:: python 

    LANGUAGE_CODE = 'en-us'
    TIME_ZONE = 'UTC'
    USE_I18N = True
    USE_TZ = True

Controls:
	- Localization
	- Time handling
	- Internationalization

🔟 Static files
-----------------

.. code-block:: python 

    STATIC_URL = 'static/'

Used for:
	- CSS
	- JavaScript
	- Images

In production, static files are served separately.

1️⃣1️⃣ Default primary key type
---------------------------------

.. code-block:: python 

    DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

Defines how primary keys are generated.

===============================================================================================================

------------------------------------
4. What NOT to do in settings.py
------------------------------------

- ❌ Put secrets directly (use environment variables)
- ❌ Hardcode production values
- ❌ Delete default sections blindly
- ❌ Mix dev & prod settings in large projects

