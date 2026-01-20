lib 
======

Contains all Python packages installed in the virtual environment. Django and its dependencies are located in site-packages. This directory is automatically managed by pip.

----------------------------
📂 djenv/lib — what is it?
----------------------------

lib/ is where all installed Python packages are stored for this virtual environment.

When you install Django, pip puts it **here.**

If bin/ is the engine, lib/ is the fuel + parts.

----------------------------
The structure may contains 
----------------------------

.. code-block:: bash 

    djenv/lib/
    └── python3.14/
        └── site-packages/
            ├── asgiref/
            ├── asgiref-3.11.0.dist-info/
            ├── django/
            ├── django-6.0.dist-info/
            ├── pip/
            ├── pip-25.3.dist-info/
            ├── sqlparse/
            └── sqlparse-0.5.5.dist-info/

Let’s break this down piece by piece 

=========================================================================================================

1️⃣ python3.14/

This folder corresponds to the Python version used by the venv.
	•	Your venv was created with Python 3.14
	•	All packages are version-scoped
	•	Prevents conflicts between Python versions

On another machine it might be python3.12 or python3.11.

========================================================================================================

2️⃣ site-packages/ (MOST IMPORTANT)

This is where:
	•	Django lives
	•	All third-party libraries live
	•	Python imports from

When you write:

.. code-block:: python 

    import django

Python looks **here.**

==========================================================================================================

3️⃣ django/

This is the Django framework source code.

Inside you’ll find:

.. code-block:: bash 

    django/
    ├── conf/
    ├── db/
    ├── http/
    ├── urls/
    ├── views/
    ├── core/
    └── ...

This is what runs when:

.. code-block:: bash 

    python manage.py runserver

You normally **do not edit this code.**

========================================================================================================

**4️⃣ django-6.0.dist-info/**

Metadata about Django:
	- Version number
	- Dependencies
	- License
	- Installed files list

Used by:
	- pip
	- package managers
	- dependency resolution

❌ Not imported by Python directly.

========================================================================================================

**5️⃣ asgiref/**

ASGI utilities used by Django for:
	- Async views
	- WebSockets
	- ASGI servers

Django depends on this.



**6️⃣ sqlparse/**

Used by Django to:
	- Format SQL queries
	- Display readable SQL in admin/debug

Not written by Django, but required by it.

========================================================================================================

**7️⃣ pip/ and pip-*.dist-info/**

pip itself lives inside the venv.

This ensures:
	- pip installs packages into this venv
	- Not into global Python

❌ What NOT to do inside lib/
	- ❌ Don’t edit Django source
	- ❌ Don’t delete random folders
	- ❌ Don’t commit to Git
	- ❌ Don’t import .dist-info

If something breaks → recreate venv.

=======================================================================================================

**How Python actually uses lib/**

When venv is active:

.. code-block:: bash 

    python

Python automatically adds:

.. code-block:: bash 

    djenv/lib/python3.14/site-packages

to sys.path.

That’s how imports work.

======================================================================================================

What happens when you install a new package?

.. code-block:: bash 

    pip install psycopg2

pip:
	1.	Downloads package

	2.	Installs it into site-packages

	3.	Adds .dist-info

	4.	Makes it importable