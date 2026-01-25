migrations
============

--------------------------------------
**What is migrations/ in Django?**
--------------------------------------

Short definition:
    Migrations are Django’s way of tracking and applying database schema changes.

In simple words:
    Migrations convert your Python models into database tables.

Summary:
    Django migrations are Python files that track and apply database schema changes based on your models.

=================================================================================================================================================

----------------------------------------
**Where migrations/ fits in Django**
----------------------------------------

Flow:

.. code-block:: bash 

    models.py  ➜  migrations  ➜  database (db.sqlite3 / PostgreSQL)

Django **never directly changes the database.**

It **always** uses migrations.

=================================================================================================================================================

---------------------------------------
**Structure of migrations/ folder**
---------------------------------------

Inside your app:

.. code-block:: bash 

    myapp/
    ├── migrations/
    │   ├── __init__.py
    │   └── 0001_initial.py   ← appears later

----------------------------
**Why this is a folder?**
----------------------------

Because Django stores **multiple migration files** over time.

=================================================================================================================================================

------------------------------------
**__init__.py inside migrations**
------------------------------------

This file:

.. code-block:: python 

    # empty

Purpose:
	- Marks migrations as a **Python package**
	- Allows Django to import migration files

You **never touch this file**

=================================================================================================================================================

-----------------------------------------
**When are migration files created?**
-----------------------------------------

Migration files are created when:
	#.	You write or change models
	#.	You run:

.. code-block:: bash 

    python manage.py makemigrations

Example:

.. code-block:: python 

    # myapp/models.py
    from django.db import models

    class Post(models.Model):
        title = models.CharField(max_length=200)
        content = models.TextField()

Run:

.. code-block:: bash 

    python manage.py makemigrations

Django creates:

.. code-block:: bash 

    migrations/
    └── 0001_initial.py

=================================================================================================================================================

-----------------------------------------
**What is inside a migration file?**
-----------------------------------------

Example 0001_initial.py:

.. code-block:: python 

    from django.db import migrations, models

    class Migration(migrations.Migration):

        initial = True

        dependencies = []

        operations = [
            migrations.CreateModel(
                name='Post',
                fields=[
                    ('id', models.BigAutoField(primary_key=True)),
                    ('title', models.CharField(max_length=200)),
                    ('content', models.TextField()),
                ],
            ),
        ]

This means:
	- Create table post
	- Add columns title, content
	- Add primary key id

=================================================================================================================================================

---------------------------------
**Two-step migration process**
---------------------------------

**Step1:** Create migration files

.. code-block:: bash 

    python manage.py makemigrations

Creates files in migrations/

**Step2:** Apply migrations to database

.. code-block:: bash 

    python manage.py migrate

➡️ Updates **db.sqlite3** (or PostgreSQL)

=================================================================================================================================================

----------------------------------------
**Migration commands you must know**
----------------------------------------

.. list-table:: 
    :header-rows: 1

    * - Command
      - Purpose
    * - makemigrations
      - Create migration files
    * - migrate
      - Apply migrations
    * - showmigrations
      - List applied/unapplied migrations
    * - sqlmigrate app 0001
      - Show SQL
    * - migrate app zero
      - Rollback app

=================================================================================================================================================

**Example real workflow**

.. code-block:: bash 

    # change models.py
    python manage.py makemigrations
    python manage.py migrate

Repeat this **every time you change models.**

=================================================================================================================================================

Common beginner mistakes: 
    - Editing database manually
    - Forgetting to run migrate
    - Deleting migration files randomly
    - Running migrate without makemigrations
    - Using migrations as version control

**Is it safe to delete migrations?**

.. list-table:: 
    :header-rows: 1

    * - Situation
      - Safe?
    * - Early development
      - ⚠️ Sometimes
    * - Production
      - ❌ NEVER
    * - Team project
      - ❌ NEVER
    * - Reset local DB
      - ⚠️ Carefully

=================================================================================================================================================

Why migrations are powerful:
    - Database versioning
    - Rollbacks
    - Team synchronization
    - Database-agnostic (SQLite → PostgreSQL → MySQL)
    - Production safe




