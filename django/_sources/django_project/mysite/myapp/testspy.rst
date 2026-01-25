tests.py 
==========

----------------------------
**What tests.py is for**
----------------------------

In Django, tests.py usually contains:
	- **Model tests** (does your model logic work?)
	- **View tests** (does your page/API return correct response?)
	- **URL tests** (does a URL resolve to the right view?)
	- **Form/serializer tests** (if you use forms or DRF)

Django uses Python’s unittest style, but Django adds helpers.

=================================================================================================================================

----------------------------
**How Django runs tests**
----------------------------

From your project folder (where manage.py is):

.. code-block:: bash 

    python manage.py test

Or only this app:

.. code-block:: bash 

    python manage.py test myapp

Django will:
	- create a **temporary test database**
	- run tests
	- delete the test database

=================================================================================================================================

---------------------------------
**Basic example in tests.py**
---------------------------------

**1) Simple test**

.. code-block:: python 

    from django.test import TestCase

    class SimpleTest(TestCase):
        def test_basic_math(self):
            self.assertEqual(1 + 1, 2)

Run:

.. code-block:: bash 

    python manage.py test

=================================================================================================================================

**Example: Test a View (page)**

**views.py**

.. code-block:: python 

    from django.http import HttpResponse

    def home(request):
        return HttpResponse("Hello")

**urls.py (inside app)**

.. code-block:: python 

    from django.urls import path
    from . import views

    urlpatterns = [
        path("", views.home, name="home"),
    ]

**tests.py**

.. code-block:: python 

    from django.test import TestCase
    from django.urls import reverse

    class HomeViewTest(TestCase):
        def test_home_returns_200(self):
            url = reverse("home")
            response = self.client.get(url)

            self.assertEqual(response.status_code, 200)
            self.assertContains(response, "Hello")
        
self.client.get() simulates a browser request.

=================================================================================================================================

**Example: Test a Model**

**models.py**

.. code-block:: python 

    from django.db import models

    class Product(models.Model):
        name = models.CharField(max_length=100)
        price = models.IntegerField()

        def is_expensive(self):
            return self.price > 100

**tests.py**

.. code-block:: python 

    from django.test import TestCase
    from .models import Product

    class ProductModelTest(TestCase):
        def test_is_expensive(self):
            p = Product.objects.create(name="Phone", price=200)
            self.assertTrue(p.is_expensive())

**Best Practice**

Even though Django gives a single tests.py, in real projects we often create:

.. code-block:: bash 

    myapp/tests/
        __init__.py
        test_models.py
        test_views.py
        test_urls.py

cleaner when tests grow








