myapp 
==========

----------------
What is myapp?
----------------

**myapp is a Django application.**

In Django:
	- A **project** = whole website (settings, config, deployment)
	- An **app** = one feature or module inside the project

Examples of apps:
	- Blog
	- Accounts
	- Products
	- Orders
	- Payments

Here myapp is a **feature container**, not the whole site.

============================================================================================================================================================================

----------------------------------
How to Create an App in Django
----------------------------------

Step0: Make sure you are in the right place
----------------------------------------------

You must be **inside the Django project directory**, where manage.py exists.

Example:

.. code-block:: bash 

   mysite/
   ├── manage.py  
   ├── mysite/

Check:

.. code-block:: bash 

   ls 

You should see:

.. code-block:: bash 

   manage.py 

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step1: Activate your virtual environment
------------------------------------------

If you’re using venv:

**macOS / Linux**

.. code-block:: bash 

   source djenv/bin/activate

**Windows**

.. code-block:: bash 

   djenv\Scripts\activate

You should see something like:

.. code-block:: bash 

   (djenv)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step2: Create the Django app
------------------------------

A Django app is created using python manage.py startapp appname, then registered in INSTALLED_APPS to become active.

Run:

.. code-block:: bash 

   python manage.py startapp myapp

Replace myapp with your app name:
	- blog
	- accounts
	- products
	- orders

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step3: What Django creates for you
-------------------------------------

After running the command, Django generates:

.. code-block:: bash 

   myapp/
   ├── migrations/
   │   └── __init__.py
   ├── __init__.py
   ├── admin.py
   ├── apps.py
   ├── models.py
   ├── tests.py
   ├── views.py

This is a **complete app skeleton.**

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step4: Register the app
---------------------------

Open:

.. code-block:: bash 

   mysite/settings.py

Find:

.. code-block:: python 

   INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      ...
   ]

Add your app:

.. code-block:: python 

   INSTALLED_APPS = [
      ...
      'myapp',
   ]

If you skip this step, Django will **ignore your app.**

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step5: Run the server to verify
---------------------------------

.. code-block:: bash 

   python manage.py runserver

Open:

.. code-block:: bash 

   http://127.0.0.1:8000/

If no errors → app created successfully

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step6: (Optional) Create app URLs
-------------------------------------

Create a file:

.. code-block:: bash 

   myapp/urls.py

Add:

.. code-block:: python 

   from django.urls import path
   from . import views

   urlpatterns = [
      path('', views.home, name='home'),
   ]

Then include it in **project urls.py:**

.. code-block:: python 

   from django.urls import path, include

   urlpatterns = [
      path('', include('myapp.urls')),
   ]

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Step7: (Optional) Create your first view
-------------------------------------------

In myapp/views.py:

.. code-block:: python 

   from django.http import HttpResponse

   def home(request):
      return HttpResponse("Hello from myapp")

Refresh browser

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Naming rules for apps
-----------------------

✅ Good names:
	- blog
	- accounts
	- payments
	- orders

❌ Bad names:
	- MyApp
	- Test-App
	- django

Use:
	- lowercase
	- no spaces
	- no hyphens

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Common mistakes to avoid
--------------------------

- ❌ Running startapp outside project
- ❌ Forgetting to add app to INSTALLED_APPS
- ❌ Using uppercase names
- ❌ Creating one giant app

============================================================================================================================================================================

-------------------
Where myapp lives
-------------------

.. code-block:: bash 

   mysite/
   ├── myapp/      ← application (features live here)
   ├── mysite/     ← project configuration
   ├── manage.py

============================================================================================================================================================================

-----------------------
Why Django uses apps
-----------------------

Django apps give you:
   - Modular design
   - Reusability
   - Clean separation of concerns
   - Easier testing
   - Enterprise-scale structure

A real Django project often has **many apps.**

============================================================================================================================================================================

-------------------------
myapp folder structure
-------------------------

.. code-block:: bash 

   myapp/
   ├── migrations/
   ├── __init__.py
   ├── admin.py
   ├── apps.py
   ├── models.py
   ├── tests.py
   ├── views.py

We will explain **each file separately**, check left sidebar navigation.

============================================================================================================================================================================

-------------------------------------
How myapp connects to the project
-------------------------------------

Nothing in myapp works until you **register it.**

In settings.py:

.. code-block:: python 

   INSTALLED_APPS = [
      ...
      'myapp',
   ]

Once added:
	- Models are recognized
	- Migrations work
	- Admin shows your models
	- URLs can connect to views

============================================================================================================================================================================

--------------------------------
What myapp is responsible for
--------------------------------

myapp can contain:
	- Database tables (models)
	- Business logic
	- Views (HTTP handling)
	- Admin customization
	- Tests
	- API logic

❌ It does NOT:
	- Configure settings
	- Run servers
	- Handle deployment

============================================================================================================================================================================

-----------------
Project vs App
-----------------

.. list-table:: 
   :header-rows: 1

   * - Project (mysite)
     - App (myapp)
   * - Settings
     - Features
   * - URLs (root)
     - URLs (feature-level)
   * - ASGI / WSGI
     - Views
   * - Deployment
     - Business logic

============================================================================================================================================================================

---------------------
Real-world example
---------------------

Think like this:
   🏢 Project = Mall

   🏬 Apps = Shops

- Mall handles security, electricity, layout
- Each shop handles its own products and sales

============================================================================================================================================================================

------------------------
How Django uses myapp
------------------------

Request flow:

.. code-block:: bash 

   Browser → urls.py → views.py → models.py → response


All of that happens **inside the app.**

============================================================================================================================================================================

-----------------------
Very important rule
-----------------------

**One app = one responsibility**

Good:
	- accounts
	- orders
	- payments

Bad:
	- One giant app doing everything

============================================================================================================================================================================

-------------------------
What we’ll cover next
-------------------------

Next pages in this exact order:
   #. migrations/
   #. __init__.py (app-level)
   #. apps.py
   #. models.py
   #. admin.py
   #. views.py
   #. tests.py








.. toctree::
   :hidden:
   :maxdepth: 7

   migrations/index
   __init__py
   adminpy
   appspy
   modelspy
   signalspy
   testspy
   urlspy
   viewspy


