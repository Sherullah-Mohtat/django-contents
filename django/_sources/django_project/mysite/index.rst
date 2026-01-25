mysite 
========

----------------------
**What is mysite?**
----------------------

mysite is the Django project directory that contains apps, the database, and a nested configuration package used by Django to run the project.

In project, **mysite appears twice**, and this is **intentional.**

Structure:

.. code-block:: bash 

   django_project/
   ├── djenv/
   └── mysite/          ← outer mysite (PROJECT ROOT)
      ├── myapp/
      ├── mysite/      ← inner mysite (DJANGO CONFIG)
      ├── db.sqlite3
      └── manage.py

Let’s break this down carefully.

===========================================================================================================

**1️⃣ Outer mysite/ (Project root)**
--------------------------------------

This folder is created when you run.

.. code-block:: bash 

   django-admin startproject mysite

This outer mysite/ is:
	- The Django project root
	- Where you run Django commands
	- NOT a Python package
	- NOT imported in code

It contains:
	- manage.py
	- apps (myapp)
	- database file
	- inner Django configuration folder

===========================================================================================================

**2️⃣ manage.py (command center)**
------------------------------------

Location:

.. code-block:: bash

   mysite/manage.py

This is the **main control script** for Django.

You use it for:

.. code-block:: bash 

   python manage.py runserver
   python manage.py startapp myapp
   python manage.py makemigrations
   python manage.py migrate
   python manage.py createsuperuser

Think of it as:

“The remote control for your Django project”

===========================================================================================================

**3️⃣ db.sqlite3 (default database)**
--------------------------------------

Location:

.. code-block:: bash 

   mysite/db.sqlite3

- Default database (SQLite)
- Used for development and learning
- Auto-created after first migration

In real projects:
	- Often replaced with PostgreSQL
	- Usually ignored in Git

===========================================================================================================

**4️⃣ myapp/ (Django app)**
----------------------------

Location:

.. code-block:: bash 

   mysite/myapp/

This is actual application code:
	- views
	- models
	- urls
	- admin

Django projects are **collections of apps**.

===========================================================================================================

**5️⃣ Inner mysite/ (Django configuration package)**
--------------------------------------------------------

Location:

.. code-block:: bash 

   mysite/mysite/

This **inner folder is the real Django configuration module.**

It **IS a Python package** and contains:

.. code-block:: bash 

   mysite/mysite/
   ├── __init__.py
   ├── settings.py
   ├── urls.py
   ├── asgi.py
   └── wsgi.py

This is where Django looks for:
	- settings
	- URL routing
	- deployment configuration

===========================================================================================================

-----------------------------------------
**Why are there TWO mysite folders?**
-----------------------------------------

This confuses almost everyone at first 

Here’s the reason:

.. list-table::
   :header-rows: 1

   * - Folder
     - Purpose
   * - outer mysite/
     - project workspace
   * - inner mysite/
     - Django settings package

Django **must** have:
	- a project directory (workspace)
	- a Python package with settings

They often share the same name by default.

You can rename the outer one if you want — Django doesn’t care.

===========================================================================================================

-------------------------------
**How Django uses mysite**
-------------------------------

When you run:

.. code-block:: bash 

   python manage.py runserver

Django:
	1.	Uses manage.py

	2.	Loads settings from mysite.settings

	3.	Reads URLs from mysite.urls

	4.	Starts the server

That mysite.settings refers to the **inner folder.**

===========================================================================================================

Analogy (very helpful)
	- 🏠 Outer mysite/ → house
	- 🧠 Inner mysite/ → brain
	- 🧱 myapp/ → rooms
	- 🕹 manage.py → remote control

===========================================================================================================

Common beginner mistakes
	- Editing files in the wrong mysite
	- Thinking outer mysite is imported
	- Deleting manage.py
	- Renaming inner mysite without updating settings

You avoided all of these 







.. toctree::
   :hidden:
   :maxdepth: 5

   myapp/index
   mysite/index 
   dbsqlite3
   managepy
  