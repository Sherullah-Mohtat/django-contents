wsgi.py
=========

--------------------------
**1. What is wsgi.py?**
--------------------------

wsgi.py is the entry point for running a Django project using WSGI servers.

WSGI = **Web Server Gateway Interface**

Location:

.. code-block:: bash 

    mysite/mysite/wsgi.py

This file allows Django to communicate with **traditional web servers** in production.

=======================================================================================================================

-----------------------------------
**2. Why does Django use WSGI?**
-----------------------------------

Before ASGI, **WSGI was the standard** for Python web applications.

It supports:
	- Synchronous HTTP requests
	- Stable production deployments
	- High performance with proven servers

Most Django apps in production still use WSGI.

**Typical contents of wsgi.py**

.. code-block:: python

    import os
    from django.core.wsgi import get_wsgi_application

    os.environ.setdefault(
        'DJANGO_SETTINGS_MODULE',
        'mysite.settings'
    )

    application = get_wsgi_application()

=======================================================================================================================

**1️⃣ Import OS utilities**
----------------------------

.. code-block:: python 

    import os

Used to set environment variables.

**2️⃣ Import Django’s WSGI handler**
-------------------------------------

.. code-block:: python 

    from django.core.wsgi import get_wsgi_application

Creates a WSGI-compatible Django application.

**3️⃣ Set the settings module**
---------------------------------

.. code-block:: python 

    os.environ.setdefault(
        'DJANGO_SETTINGS_MODULE',
        'mysite.settings'
    )

Tells Django which settings file to load.

**4️⃣ Create the WSGI application**
-------------------------------------

.. code-block:: python 

    application = get_wsgi_application()

This application object is what the web server runs.

=======================================================================================================================

--------------------------------------------
**3. How wsgi.py is used in real life**
--------------------------------------------

Used with servers like:
	- Gunicorn
	- uWSGI
	- mod_wsgi (Apache)

Example:

.. code-block:: bash 

    gunicorn mysite.wsgi:application

=======================================================================================================================

----------------------
**4. WSGI vs ASGI**
----------------------

.. list-table::
    :header-rows: 1

    * - Feature
      - WSGI
      - ASGI
    * - Request type
      - Sync
      - Sync + Async
    * - WebSockets
      - ❌ No
      - ✅ Yes
    * - HTTP support
      - ✅ Yes
      - ✅ Yes
    * - Maturity
      - Very stable
      - Modern
    * - Django default
      - ✅ Yes
      - Optional

=======================================================================================================================

------------------------------
**4. Do you need wsgi.py?**
------------------------------

For development
	- Django uses its own dev server
	- You don’t need to touch wsgi.py

For production
	- Yes, absolutely
	- Most hosting providers expect WSGI

What happens if you delete wsgi.py?
	- Production deployment will fail
	- Some servers won’t start
	- Django loses its WSGI entry point

Never delete it.

**What wsgi.py is NOT**

- Not URL routing
- Not async handling
- Not business logic
- Not middleware

It is **only a bridge** between Django and a web server.

Common beginner mistakes
	- Editing wsgi.py unnecessarily
	- Confusing it with asgi.py
	- Trying to put logic inside it
	- Running it without a WSGI server





