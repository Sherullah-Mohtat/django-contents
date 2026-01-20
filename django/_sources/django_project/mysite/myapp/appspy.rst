apps.py 
=========

--------------------
What is apps.py?
--------------------

apps.py defines configuration, startup behavior and metadata for a Django app.

It tells Django:
	- What this app is called
	- How it should be loaded
	- Where startup logic (if any) belongs

Location:

.. code-block:: bash 

    myapp/apps.py

================================================================================================================================

------------------------------------
Default apps.py (auto-generated)
------------------------------------

When you run:

.. code-block:: bash 

    python manage.py startapp myapp

Django creates:

.. code-block:: python 

    from django.apps import AppConfig

    class MyappConfig(AppConfig):
        default_auto_field = 'django.db.models.BigAutoField'
        name = 'myapp'

================================================================================================================================

**Let’s break it down line by line**

**1️⃣ from django.apps import AppConfig**

This imports Django’s **application configuration base class.**

Every Django app **must** extend AppConfig.

================================================================================================================================

**2️⃣ class MyappConfig(AppConfig):**

This defines **your app’s configuration class.**

Think of it as:
    🪪 “App identity card”

================================================================================================================================

**3️⃣ name = 'myapp'**

This is the **full Python path** to the app.

Examples:

.. code-block:: python 

    name = 'myapp'
    name = 'blog'
    name = 'accounts'

For `nested apps <../../../tutorials/.nestedapp.html>`_:

.. code-block:: python 

    name = 'project.apps.blog'

================================================================================================================================

**4️⃣ default_auto_field**

.. code-block:: python 

    default_auto_field = 'django.db.models.BigAutoField'

This controls:
	- The default type of primary key (id)
	- Used when you don’t explicitly define one

BigAutoField = 64-bit integer

Safe for large datasets

Django default since 3.2+

================================================================================================================================

-------------------------------
Why does Django need apps.py?
-------------------------------

Django loads apps in this order:
	#.	Reads INSTALLED_APPS
	#.	Loads each app’s AppConfig
	#.	Initializes models, `signals <signalspy.html>`_, admin, etc.

So apps.py is the **entry point** for an app.

================================================================================================================================

------------------------------------
Connecting apps.py to settings.py
------------------------------------

In settings.py:

❌ Old style:

.. code-block:: python 

    INSTALLED_APPS = [
        'myapp',
    ]

✅ Recommended:

.. code-block:: python 

    INSTALLED_APPS = [
        'myapp.apps.MyappConfig',
    ]

Why?
	- Explicit
	- More control
	- Required for advanced features

================================================================================================================================

------------------------------
Where to put startup code?
------------------------------

If you need code to run **when Django starts**, use ready().

.. code-block:: python 

    class MyappConfig(AppConfig):
        default_auto_field = 'django.db.models.BigAutoField'
        name = 'myapp'

        def ready(self):
            import myapp.signals

Common uses:
	- Register signals
	- Startup checks
	- App initialization

================================================================================================================================

---------------------------------
What should NOT go in apps.py?
---------------------------------

❌ Views

❌ Models

❌ Business logic

❌ Database queries

apps.py is for **configuration only.**

================================================================================================================================

--------------------------
Real-world mental model
--------------------------

Think of apps.py as:
    “App bootloader”

Just like:
	- main() in C
	- package.json metadata in Node
	- Info.plist in iOS

================================================================================================================================

--------------------------
Common beginner mistakes
--------------------------

.. list-table:: 
    :header-rows: 1

    * - Mistake
      - Why it’s wrong
    * - Ignoring apps.py
      - Needed for clean app loading
    * - Putting logic inside it
      - Violates separation of concerns
    * - Not using AppConfig in INSTALLED_APPS
      - Limits extensibility







