urls.py
========

---------------------
1. What is urls.py?
---------------------

urls.py defines how URLs are mapped to views in a Django project.

Location:

.. code-block:: bash 

    mysite/mysite/urls.py

It acts as the **traffic controller** of your web application.

============================================================================================

-------------------------------------
2. What problem does urls.py solve?
-------------------------------------

When a user visits a URL like:

.. code-block:: bash 

    http://127.0.0.1:8000/admin/

Django needs to know:
	- Which Python function should run?
	- Which page should be shown?

That mapping is done in urls.py.

============================================================================================

Typical contents of urls.py

.. code-block:: python 

    from django.contrib import admin
    from django.urls import path

    urlpatterns = [
        path('admin/', admin.site.urls),
    ]

============================================================================================

1️⃣ Import admin site
----------------------

.. code-block:: python 

    from django.contrib import admin

Enables Django’s built-in admin interface.

2️⃣ Import path
----------------

.. code-block:: python 

    from django.urls import path

Used to define URL patterns.

3️⃣ URL patterns list
----------------------

.. code-block:: python 

    urlpatterns = [
        path('admin/', admin.site.urls),
    ]

- urlpatterns is required
- Django scans this list from top to bottom
- First match wins

============================================================================================

How URL routing works (important)

Example:

.. code-block:: python 

    path('myapp/', myapp_view)

If user visits:

.. code-block:: bash 

    /myapp/

Django calls:

myapp_view(request)

============================================================================================

**URL routing flow**

.. code-block:: bash 

    Browser → urls.py → View → Response

urls.py decides **which view handles the request.**

**Using apps inside urls.py**

In real projects, you don’t put everything here.

**Project-level urls.py**

.. code-block:: python 

    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('myapp.urls')),
    ]

App-level urls.py (inside myapp/)

.. code-block:: python 

    from django.urls import path
    from .views import home

    urlpatterns = [
        path('', home, name='home'),
    ]

This keeps URLs organized.

============================================================================================

URL parameters example

.. code-block:: python 

    path('post/<int:id>/', post_detail)

URL:

.. code-block:: bash 

    /post/5/

View receives:

.. code-block:: python 

    def post_detail(request, id):
    ...

Why order matters

.. code-block:: python

    urlpatterns = [
        path('', home),
        path('admin/', admin.site.urls),
    ]

If '' is first, it may catch everything.

Always put **specific paths before general ones.**

============================================================================================

**What urls.py is NOT**

- ❌ Not a view
- ❌ Not HTML
- ❌ Not database logic
- ❌ Not middleware

It only handles URL → view mapping.

============================================================================================

Common beginner mistakes
	- Forgetting urlpatterns
	- Misspelling view names
	- Not using include()
	- Putting business logic here


