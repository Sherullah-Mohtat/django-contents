asgi.py
========

----------------------
1. What is asgi.py?
----------------------

asgi.py is the entry point for running Django using ASGI servers.

ASGI = **Asynchronous Server Gateway Interface**

Location:

.. code-block:: bash 

    mysite/mysite/asgi.py

It allows Django to handle:
	- Asynchronous requests
	- WebSockets
	- Long-lived connections
	- Real-time features

======================================================================================================

--------------------------------------
2. Why does Django include asgi.py?
--------------------------------------

Modern web applications often need:
	- Chat systems
	- Live notifications
	- Streaming
	- Async APIs

ASGI is the modern standard that supports all of this.

Django includes asgi.py **by default** to support async features.

======================================================================================================

--------------------------------
3. Typical contents of asgi.py
--------------------------------

.. code-block:: python

    import os
    from django.core.asgi import get_asgi_application

    os.environ.setdefault(
        'DJANGO_SETTINGS_MODULE',
        'mysite.settings'
    )

    application = get_asgi_application()

======================================================================================================

1️⃣ Import OS utilities
-----------------------

.. code-block:: python 

    import os

Used to set environment variables.

2️⃣ Import Django’s ASGI handler
---------------------------------

.. code-block:: python 

    from django.core.asgi import get_asgi_application

This function creates an ASGI-compatible Django application.

3️⃣ Set the settings module
----------------------------

.. code-block:: python 

    os.environ.setdefault(
        'DJANGO_SETTINGS_MODULE',
        'mysite.settings'
    )

Tells Django which settings file to use.

4️⃣ Create the ASGI application
--------------------------------

.. code-block:: python

    application = get_asgi_application()

This application object is what ASGI servers run.

======================================================================================================

------------------------------------
4. How asgi.py is used in real life
------------------------------------

Used with ASGI servers like:
	- Uvicorn
	- Daphne
	- Hypercorn

Example:

.. code-block:: bash 

    uvicorn mysite.asgi:application

======================================================================================================

-----------------
5. ASGI vs WSGI
-----------------

.. list-table::
    :header-rows: 1

    * - Feature
      - ASGI
      - WSGI
    * - Async support
      - ✅ Yes
      - ❌ No
    * - WebSockets
      - ✅ Yes
      - ❌ No
    * - Long connections
      - ✅ Yes
      - ❌ No
    * - Traditional HTTP
      - ✅ Yes
      - ✅ Yes
    * - Modern standard
      - ✅ Yes
      - ❌ Older

======================================================================================================

**Do you need asgi.py right now?**

For a learning project:
	- You don’t need to touch it
	- Django uses WSGI by default

For modern apps:
	- ASGI is recommended
	- Required for real-time features

======================================================================================================

What happens if you delete asgi.py?
	- Django will still run (using WSGI)
	- But async features won’t work
	- Some deployment setups will fail

Best practice:
    **Never delete it**

======================================================================================================

Common beginner mistakes
	- Confusing ASGI with WSGI
	- Editing this file unnecessarily
	- Thinking it replaces urls.py
	- Running ASGI without an ASGI server

