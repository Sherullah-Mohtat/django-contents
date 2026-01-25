mysite 
=========

-------------------------------
**1. What is this mysite/?**
-------------------------------

The **inner mysite/ directory** is the configuration package for a Django project. It contains global settings, URL routing, and server interface definitions required to run the application.

Location:

.. code-block:: bash 

   django_project/
   └── mysite/
      ├── myapp/
      ├── mysite/   ← THIS ONE
      ├── db.sqlite3
      └── manage.py

This folder is:
	-  A **Python package**
	-  Imported by Django
	-  Contains all global project configuration

========================================================================================================

-------------------------------------------
**2. Why does Django need this folder?**
-------------------------------------------

Django needs a **central place** to define:
	- Project settings
	- URL routing
	- Server interfaces (ASGI / WSGI)

This inner mysite/ provides exactly that.

========================================================================================================

**Contents of inner mysite/**

.. code-block:: bash 

   mysite/mysite/
   ├── __init__.py
   ├── settings.py
   ├── urls.py
   ├── asgi.py
   └── wsgi.py

Each file has **one clear responsibility.**

========================================================================================================

**High-level purpose of each file**

1️⃣ __init__.py
	- Marks this folder as a Python package
	- Allows imports like:

.. code-block:: bash 

   import mysite.settings

- Usually empty

========================================================================================================

2️⃣ settings.py
	- The **heart of the project**
	- Defines:
	   - Installed apps
	   - Database
	   - Middleware
	   - Templates
	   - Static files
	   - Security settings

Django **cannot run** without this file.

========================================================================================================

3️⃣ urls.py
	- The URL routing table
	- Maps URLs → views
	- Controls what users see when they visit paths like:

.. code-block:: bash 

   /admin/
   /
   /blog/

========================================================================================================

4️⃣ asgi.py
	- Entry point for **ASGI servers**
	- Used for:
	   - Async views
	   - WebSockets
	   - Real-time features

Modern Django supports ASGI by default.

========================================================================================================

5️⃣ wsgi.py
	- Entry point for WSGI servers
	- Used in traditional deployments:
	   - Gunicorn
	   - uWSGI
	   - Apache

This is how Django runs in production (classic way).

========================================================================================================

**How Django uses this folder**

When you run:

.. code-block:: bash 

   python manage.py runserver

Django:
	1.	Loads settings from mysite.settings
	2.	Loads URLs from mysite.urls
	3.	Initializes middleware
	4.	Starts the server

The **inner mysite/** is referenced everywhere.


What you should NOT do
	- Don’t delete this folder
	- Don’t rename it without updating settings
	- Don’t move files out of it randomly




.. toctree::
   :hidden:
   :maxdepth: 5

   __init__py
   asgipy
   settingspy
   urlspy
   wsgipy
   