__init__.py 
=============

---------------------------
**What is __init__.py?**
---------------------------

__init__.py marks a directory as a Python package and allows Django to import and manage project components correctly.

Short definition:
    __init__.py tells Python: **“This folder is a Python package.”**

Without it, Python would not treat the folder as importable code.

=====================================================================================================================

-------------------------------------------------
**Where you see __init__.py in your project**
-------------------------------------------------

In your Django project, it appears in many places:

.. code-block:: bash 

    mysite/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    ├── wsgi.py

    myapp/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── views.py

    migrations/
    ├── __init__.py

Each one has a **slightly different role**, but the core idea is the same.

=====================================================================================================================

------------------------------
**Why __init__.py exists**
------------------------------

Python organizes code using **packages.**

Example:

.. code-block:: python 

    import myapp.models

Python can only do this if:
    - ✔ myapp/ is a package
    - ✔ __init__.py exists inside it

=====================================================================================================================

-----------------------------------------------
**What happens if __init__.py is missing?**
-----------------------------------------------

**Older Python (≤3.2)**

Folder is NOT a package

Imports fail

**Modern Python (3.3+)**

✔ Namespace packages exist

But Django still **expects** __init__.py

**Django best practice: always keep it**

=====================================================================================================================

-----------------------------------
**What is inside __init__.py?**
-----------------------------------

Most of the time:

.. code-block:: python 

    # empty

And that is **100% correct**

Empty does NOT mean useless.

=====================================================================================================================

--------------------------------------------
**What does Django use __init__.py for?**
--------------------------------------------

**1️⃣ Package recognition**

Django imports apps, settings, models, migrations — all via packages.

**2️⃣ App loading**

Django uses INSTALLED_APPS:

.. code-block:: python 

    INSTALLED_APPS = [
        'myapp',
    ]

Django internally imports:

.. code-block:: python 

    import myapp

➡️ __init__.py enables this.

**3️⃣ Migrations discovery**

Django scans:

.. code-block:: python 

    myapp.migrations

Without __init__.py, migrations break.

=====================================================================================================================

----------------------------------------------
**Advanced usage (OPTIONAL, but powerful)**
----------------------------------------------

You **can** put code in __init__.py, but you must be careful.

**Example: shortcut imports**

.. code-block:: python 

    # myapp/__init__.py
    from .models import Post

Now you can do:

.. code-block:: python 

    from myapp import Post

Instead of:

.. code-block:: python 

    from myapp.models import Post

=====================================================================================================================

**Example: default app config (older Django)**

.. code-block:: python 

    default_app_config = 'myapp.apps.MyappConfig'

Mostly obsolete in modern Django, but still exists in legacy code.

**What you should NOT do**

Heavy logic

Database queries

API calls

Side effects

Why?
    Because __init__.py runs **as soon as the package is imported.**

=====================================================================================================================

**__init__.py in migrations folder**

.. code-block:: bash 

    migrations/__init__.py

Purpose:
	- Marks migrations as a package
	- Allows Django to auto-discover migration files

You **never touch this file.**

=====================================================================================================================

**Simple mental model**

Think of __init__.py as:
    “Package start file”

Just like:
	- main() in C
	- index.js in Node
	- __init__.py in Python packages



