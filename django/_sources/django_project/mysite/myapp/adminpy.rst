admin.py 
==========

-------------------------
**What is admin.py?**
-------------------------

admin.py is where you connect your app’s models to Django’s built-in admin panel.

It controls:
	- What models appear in /admin
	- How they are displayed
	- How admins create, edit, search, and filter data

Location:

.. code-block:: bash 

    myapp/admin.py

Summary:
    admin.py connects your app’s models to Django’s built-in admin interface and controls how data is managed by administrators.
    
==============================================================================================================================================

-----------------------------
**What is Django Admin?**
-----------------------------

Django provides a ready-made admin interface out of the box.

After running:

.. code-block:: bash 

    python manage.py createsuperuser
    python manage.py runserver

You can access:

.. code-block:: bash 

    http://127.0.0.1:8000/admin/

➡️ admin.py controls what you see there.

==============================================================================================================================================

--------------------------------
**Default admin.py content**
--------------------------------

When you create an app, Django generates:

.. code-block:: python

    from django.contrib import admin

    # Register your models here.

This means:
    - No models are registered yet
    - Nothing from this app appears in the admin panel

==============================================================================================================================================

----------------------------------
**Registering a model (basic)**
----------------------------------

**Example model:**

.. code-block:: python 
        
    # models.py
    from django.db import models

    class Product(models.Model):
        name = models.CharField(max_length=100)
        price = models.IntegerField()

        def __str__(self):
            return self.name

**Register it in admin.py:**

.. code-block:: python 

    from django.contrib import admin
    from .models import Product

    admin.site.register(Product)

Now Product appears in the admin panel

==============================================================================================================================================

-------------------------------------------
**What does admin.site.register() do?**
-------------------------------------------

It tells Django:
    “This model should be manageable through the admin interface.”

That’s it. Simple and powerful.

==============================================================================================================================================

--------------------------------------
**Customizing admin (recommended)**
--------------------------------------

Instead of plain registration, use ModelAdmin.

.. code-block:: python 

    from django.contrib import admin
    from .models import Product

    @admin.register(Product)
    class ProductAdmin(admin.ModelAdmin):
        list_display = ("name", "price")
        search_fields = ("name",)
        list_filter = ("price",)

Now the admin panel has:
	- Columns
	- Search box
	- Filters

==============================================================================================================================================

--------------------------------
**Common ModelAdmin options**
--------------------------------

.. list-table::
    :header-rows: 1

    * - Option
      - Purpose
    * - list_display
      - Columns shown in list view
    * - search_fields
      - Enables search
    * - list_filter
      - Sidebar filters
    * - ordering
      - Default sort order
    * - readonly_fields
      - Read-only fields
    * - list_per_page
      - Pagination size

==============================================================================================================================================

-------------------------
**Admin is for WHO?**
-------------------------

Admin is for:
	- Site owners
	- Internal staff
	- Moderators
	- Content managers

Not for public users

Not a replacement for frontend UI

==============================================================================================================================================

--------------------------------------------
**Should business logic go in admin.py?**
--------------------------------------------

NO

Admin should:
	- Display data
	- Manage data

Business logic belongs in:
	- models.py
	- services.py (advanced projects)
	- views.py

==============================================================================================================================================

---------------------------------
**What if I delete admin.py?**
---------------------------------

Technically Django won’t crash, but:
	- You lose admin configuration
	- App models won’t appear in admin
	- Very bad for productivity

Always keep it.

==============================================================================================================================================

-------------------------------
**Real-world mental model**
-------------------------------

Think of admin.py as:
    🏢 “Back-office control panel”

Just like:
	- WordPress admin dashboard
	- Shopify admin panel
	- Firebase console







