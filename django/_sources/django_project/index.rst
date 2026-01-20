Django-Project
================

---------------------------------
1. What is django_project here?
---------------------------------

django_project is just a folder you created to organize your work; it is not a Django project. The real Django project is mysite.

**django_project is NOT a Django thing.**

It is simply a **folder I created.**

Think of it as a **workspace / container / root directory** for everything related to this project.

**Big picture**

There are **3 different levels** here:

.. code-block:: bash 

   django_project   ← My folder (workspace / root)
   ├── djenv        ← Python virtual environment
   └── mysite       ← Django project (created by Django)

Only **mysite** is a real Django project.

===========================================================================================================================

1️⃣ django_project/ (top-level folder)
--------------------------------------

This is:
	- Your **personal project folder**
	- Created by **me**, not Django
	- Holds **everything related** to this work

Purpose:
	- Keep venv
	- Keep Django code
	- Keep future files (docs, notes, scripts)

You could name it anything:
	- django_project
	- django_learning
	- contents_blog
	- sherullah_django

Django does **not care** about this folder name.

===========================================================================================================================

2️⃣ djenv/ (virtual environment)
--------------------------------

This folder contains:
	- Python executable
	- pip
	- Django installation
	- All Python packages

Why it lives here:
	- Project isolation
	- Clean system Python
	- Easy deletion (rm -rf djenv)

This is why your IDE shows **External Libraries** linked to djenv.

===========================================================================================================================

3️⃣ mysite/ (actual Django project)
-----------------------------------

This is created by:

.. code-block:: bash 

   django-admin startproject mysite

Inside mysite/:

.. code-block:: bash 

   mysite/
   ├── manage.py
   └── mysite/
      ├── settings.py
      ├── urls.py
      ├── asgi.py
      └── wsgi.py

THIS is the real Django project.

===========================================================================================================================

**❗ Important clarification**

.. list-table::
   :header-rows: 1

   * - Name
     - What it really is
   * - django_project
     - ❌ Not Django, just a folder
   * - djenv
     - 🐍 Python virtual environment
   * - mysite
     - ✅ Django project
   * - myapp
     - ✅ Django app

===========================================================================================================================

**Simple analogy (real life)**

Think of it like this:
	- 🏠 **django_project** → Your house
	- 🧰 **djenv** → Your toolbox
	- 🏗 **mysite** → The building you’re constructing
	- 🧱 **myapp** → Rooms inside the building





.. toctree::
   :hidden:
   :maxdepth: 2

   djenv/index
   mysite/index 
   



