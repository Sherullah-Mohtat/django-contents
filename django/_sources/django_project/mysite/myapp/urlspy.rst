urls.py
=========

------------------------------------
**What is urls.py (in an app)?**
------------------------------------

urls.py answers this question:
    When a user opens a URL, which view should run?

Example:

.. code-block:: bash

    /           → home view
    /products/ → products view

======================================================================================================================================

------------------------------------------
**Where myapp/urls.py fits in Django**
------------------------------------------

There are **two levels of URLs:**

1️⃣ Project-level (mysite/urls.py)
	- Main router
	- Includes app URLs

2️⃣ App-level (myapp/urls.py)
	- App’s own routes
	- Clean and reusable

======================================================================================================================================

---------------------------------------
**Basic structure of myapp/urls.py**
---------------------------------------

.. code-block:: python 

    from django.urls import path
    from . import views

    urlpatterns = [
        path("", views.home, name="home"),
    ]

**Explanation:**

.. list-table:: 
    :header-rows: 1

    * - Part
      - Meaning
    * - path()
      - Define a URL pattern
    * - ""
      - Empty path → app root
    * - views.home
      - Function to execute
    * - name="home"
      - URL name (used by reverse)

======================================================================================================================================

**Example: Create a simple view**

**views.py**

.. code-block:: python 

    from django.http import HttpResponse

    def home(request):
        return HttpResponse("Hello from myapp")

======================================================================================================================================

-----------------------------------------
**Connect app URLs to project URLs**
-----------------------------------------

mysite/urls.py

.. code-block:: python 

    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path("admin/", admin.site.urls),
        path("", include("myapp.urls")),
    ]

This line:

.. code-block:: python 

    path("", include("myapp.urls"))

means:
    “Send requests to myapp’s urls.py”

======================================================================================================================================

**Final URL result**

.. list-table:: 
    :header-rows: 1

    * - URL
      - What happens
    * - http://127.0.0.1:8000/
      - runs views.home()
    * - http://127.0.0.1:8000/admin/
      - Django admin

======================================================================================================================================

-------------------------------------
**Multiple URLs in myapp/urls.py**
-------------------------------------

.. code-block:: python 

    urlpatterns = [
        path("", views.home, name="home"),
        path("about/", views.about, name="about"),
        path("contact/", views.contact, name="contact"),
    ]

======================================================================================================================================

**URL parameters**

**URL with ID**

.. code-block:: python 

    path("product/<int:id>/", views.product_detail, name="product_detail")

**View**

.. code-block:: python 

    def product_detail(request, id):
        return HttpResponse(f"Product ID: {id}")

Example URL:

.. code-block:: bash 

    /product/5/

======================================================================================================================================

**URL Names & reverse()**

Why names matter:

.. code-block:: python 

    from django.urls import reverse
    reverse("home")

This avoids **hardcoding URLs.**

**Mental Model** 

Think of urls.py as:

.. code-block:: bash 

    URL → View → Response

.. code-block:: bash 

    Browser
      ↓
    urls.py
      ↓
    views.py
      ↓
    HTML / JSON / Text

======================================================================================================================================

**Common Mistakes**

Forgetting to include app URLs in project

Writing logic in urls.py

Hardcoding URLs instead of using names


**Best Practice (Production)**

.. code-block:: bash 

    myapp/
        urls.py
        views/
            __init__.py
            home.py
            products.py

Keeps large apps clean.




