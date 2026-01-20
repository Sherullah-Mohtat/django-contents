models.py 
===========

---------------------
What is models.py?
---------------------

models.py defines the structure of your database using Python classes, allowing Django to automatically create, update, and manage database tables through migrations.

In Django:
	- You **do not write SQL directly**
	- You define **Models**
	- Django **creates tables automatically**

Think of it as:
    Python classes → Database tables

======================================================================================================================================

---------------
Mental Model
---------------

.. list-table::
    :header-rows: 1

    * - Django
      - Database
    * - Model class
      - Table
    * - Model field
      - Column
    * - Model instance
      - Row
    * - ForeignKey
      - Relationship
    * - Migration
      - SQL version control

======================================================================================================================================

-------------------------------
Basic structure of models.py
-------------------------------

.. code-block:: python 

    from django.db import models

This imports Django’s ORM (Object-Relational Mapper).

======================================================================================================================================

**Small example**

**1️⃣ Define a model**

.. code-block:: python 

    class Product(models.Model):
        name = models.CharField(max_length=100)
        price = models.DecimalField(max_digits=8, decimal_places=2)
        created_at = models.DateTimeField(auto_now_add=True)

What happens?

.. list-table:: 
    :header-rows: 1

    * - Line
      - Meaning
    * - class Product
      - Table name: product
    * - models.Model
      - Base ORM class
    * - CharField
      - VARCHAR
    * - DecimalField
      - DECIMAL
    * - DateTimeField
      - TIMESTAMP

======================================================================================================================================

**2️⃣ Django auto-generates SQL**

You never write:

.. code-block:: sql 

    CREATE TABLE product (...)

Django does it via **migrations.**

======================================================================================================================================

**Models → Migrations → Database**

The lifecycle:

.. code-block:: bash 

    models.py
      ↓
    makemigrations
      ↓
    migration files
      ↓
    migrate
      ↓
    database tables

======================================================================================================================================

--------------------------
Field Types (core ones)
--------------------------

.. list-table:: 
    :header-rows: 1

    * - Field
      - Use
    * - CharField
      - Short text
    * - TextField
      - Long text
    * - IntegerField
      - Numbers
    * - BooleanField
      - True/False
    * - DateTimeField
      - Dates
    * - ForeignKey
      - Relations
    * - ManyToManyField
      - Many-to-many

======================================================================================================================================

**🔗 Relationships**

**ForeignKey** (One-to-Many)

.. code-block:: python 

    class Order(models.Model):
        product = models.ForeignKey(Product, on_delete=models.CASCADE)

Meaning:
	- One product → many orders

======================================================================================================================================

**ManyToManyField** (`Many-to-Many <../../../tutorials/.many_to_many.html>`_)

.. code-block:: python 

    class Student(models.Model):
        courses = models.ManyToManyField("Course")

======================================================================================================================================

Naming rules (best practice):
    - ✔ Singular model names
    - ✔ CamelCase class names
    - ✔ snake_case field names

Good:

.. code-block:: python 

    class UserProfile(models.Model):

Bad:

.. code-block:: python 

    class users(models.Model):

======================================================================================================================================

**__str__() (important for admin)**

.. code-block:: python 

    def __str__(self):
        return self.name

This controls:
	- Admin display
	- Debugging
	- Django shell readability

======================================================================================================================================

`Meta options <../../../tutorials/.class_meta.html>`_ (advanced but important)

.. code-block:: python

    class Product(models.Model):
        name = models.CharField(max_length=100)
        class Meta:
            ordering = ["-created_at"]
            db_table = "products"

======================================================================================================================================

How models connect to other files

.. list-table:: 
    :header-rows: 1

    * - File
      - Relation
    * - models.py
      - Defines schema
    * - admin.py
      - Displays models
    * - views.py
      - Reads/writes models
    * - serializers.py
      - (DRF) API layer
    * - migrations/
      - DB versioning

======================================================================================================================================

Common beginner mistakes:
    - ❌ Editing migration files manually
    - ❌ Forgetting makemigrations
    - ❌ Changing models without migrating
    - ❌ Importing models incorrectly

**Real-world analogy**

Think of models.py as:
    Architectural blueprint of a building

    If you change the blueprint → rebuild (migrate)









