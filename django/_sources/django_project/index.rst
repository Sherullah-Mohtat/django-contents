Django-Project
================

-------------------------------------
**1. What is django_project here?**
-------------------------------------

django_project is just a folder I created to organize my work; it is not a Django project. The real Django project is mysite.

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

**1️⃣ django_project/ (top-level folder)**
-------------------------------------------

This is:
	- My **personal project folder**
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

**2️⃣ djenv/ (virtual environment)**
---------------------------------------

This folder contains:
	- Python executable
	- pip
	- Django installation
	- All Python packages

Why it lives here:
	- Project isolation
	- Clean system Python
	- Easy deletion (rm -rf djenv)

===========================================================================================================================

**3️⃣ mysite/ (actual Django project)**
------------------------------------------

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

**Important clarification**

.. list-table::
   :header-rows: 1

   * - Name
     - What it really is
   * - django_project
     - Not Django, just a folder
   * - djenv
     - Python virtual environment
   * - mysite
     - Django project
   * - myapp
     - Django app

===========================================================================================================================

**Simple analogy (real life)**

Think of it like this:
	- 🏠 **django_project** → Your house
	- 🧰 **djenv** → Your toolbox
	- 🏗 **mysite** → The building you’re constructing
	- 🧱 **myapp** → Rooms inside the building

===========================================================================================================================

-----------------------------------------------
**Practical: Creating This Django Project**
-----------------------------------------------

Now that you understand **what each folder means,**

let’s create the same structure step by step using real commands.

Before creating a Django project, your system must have **Python installed.**

Why Python is required
	- Django is written in **Python**
	- Django runs **on top of Python**
	- All Django commands use Python internally

**No Python = No Django**

**Check if Python is already installed**

**macOS / Linux**

.. code-block:: bash 

  python3 --version

**Windows**

.. code-block:: bash 

  python --version

Expected output:

.. code-block:: bash 

  Python 3.10.x

Django officially supports Python 3.x

Python 2 is not supported

===========================================================================================================================

Then place **all commands here:**

.. code-block:: bash 

  mkdir django_project
  cd django_project

.. code-block:: bash 

  python3 -m venv djenv
  source djenv/bin/activate

.. code-block:: bash 

  pip install django
  django-admin startproject mysite
  cd mysite
  python manage.py startapp myapp


**Install PostgreSQL driver for Django**

.. code-block:: bash 

  pip install "psycopg[binary]"

.. toctree::
   :hidden:
   :maxdepth: 2

   djenv/index
   mysite/index 
   



