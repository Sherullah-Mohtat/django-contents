djenv 
=======

-----------------------
**1. What is djenv?**
-----------------------

**djenv is a Python virtual environment (venv).**

It is:
	- Created by **me**
	- Not created by Django
	- Not part of Django code
	- Used to isolate Python + Django + packages

Command you used:

.. code-block:: bash 

   python3 -m venv djenv

=======================================================================================================

---------------------------
**2. Why djenv exists**
---------------------------

Without a virtual environment:
	- Django installs globally
	- Version conflicts happen
	- Projects break each other

With djenv:
	- Each project has **its own Python world**
	- You can delete it anytime
	- Safe for learning & production

**One project = one venv**

=======================================================================================================

**📁 What’s inside djenv**

.. code-block:: bash 

   djenv/
   ├── bin/
   ├── include/
   ├── lib/
   ├── pyvenv.cfg
   └── .gitignore

=======================================================================================================

**1️⃣ bin/**

This is the **heart** of the virtual environment.

Contains:
	- python
	- pip
	- django-admin
	- activate

**Key files you’ll use:**

.. code-block:: bash 

   djenv/bin/activate
   djenv/bin/python
   djenv/bin/pip

**When you run:**

.. code-block:: bash 

   source djenv/bin/activate

You are telling the system:

“From now on, use Python and pip from THIS folder.”

That’s why your terminal shows:

.. code-block:: bash 

   (djenv)

=======================================================================================================

**2️⃣ lib/**

This is where **all installed Python packages live.**

After:

.. code-block:: bash 

   pip install Django

Django is installed here:

.. code-block:: bash 

   djenv/lib/python3.x/site-packages/django/

Nothing here should be edited manually.

=======================================================================================================

**3️⃣ include/**

Used for:
	- C headers
	- Native extensions

You usually **never touch this.**

=======================================================================================================

**4️⃣ pyvenv.cfg**

This file describes the virtual environment.

Example contents:

.. code-block:: bash 

   home = /usr/bin/python3
   include-system-site-packages = false
   version = 3.x.x

Meaning:
	- Which Python created the venv
	- Whether global packages are allowed

=======================================================================================================

**5️⃣ .gitignore**

Prevents committing venv files to Git.

**Never push djenv to GitHub.**

Instead, use:

.. code-block:: bash 

   requirements.txt

=======================================================================================================

**🔁 How djenv is used (daily workflow)**

Activate

.. code-block:: bash 

   source djenv/bin/activate

Install packages

.. code-block:: bash 

   python -m pip install Django

Run Django

.. code-block:: bash

   python manage.py runserver

Deactivate

.. code-block:: bash 

   deactivate 

=======================================================================================================

**Relationship between djenv and Django**

.. list-table::
   :header-rows: 1
   
   * - Item
     - Role
   * - djenv
     - Python environment
   * - Django
     - Installed inside djenv
   * - mysite
     - Django project
   * - myapp
     - Django app

Django **runs using Python from djenv.**

=======================================================================================================

**What djenv is NOT**
   - Not Django project
   - Not Django app
   - Not settings
   - Not production code

It is just an **isolated runtime environment.**

=======================================================================================================

**Analogy (easy to remember)**
	- 🧰 djenv → toolbox
	- 🏗 mysite → building
	- 🧱 myapp → rooms inside the building

.. toctree::
   :hidden:
   :maxdepth: 5

   bin/index
   include/index 
   lib/index 
   .gitignore
   pyvenvcfg



