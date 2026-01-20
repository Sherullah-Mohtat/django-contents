db.sqlite3
============

------------------------
1. What is db.sqlite3?
------------------------

db.sqlite3 is the default SQLite database used by Django during development. It stores all application data in a single file and is suitable for learning and local testing.

It is a **SQLite database**, stored as a **single file** on disk.

Location:

.. code-block:: bash 

    mysite/db.sqlite3

=======================================================================================================

---------------------------------------
2. Why does Django create db.sqlite3?
---------------------------------------

When you create a new Django project, Django configures SQLite as the default database because:
	-  No installation required
	-  Easy to use
	-  Perfect for learning and development
	-  Works out of the box

Django automatically creates this file **after you run migrations.**

=======================================================================================================

--------------------------------
3. When is db.sqlite3 created?
--------------------------------

The file appears when you run:

.. code-block:: bash 

    python manage.py migrate

Django then:
	- Creates database tables
	- Stores them in db.sqlite3

=======================================================================================================

----------------------------------
4. What does db.sqlite3 contain?
----------------------------------

It stores all **project data**, including:
	- Django system tables
	- User accounts
	- Admin data
	- Your app’s models
	- Migration history

Examples of tables inside:
	- auth_user
	- django_migrations
	- django_admin_log
	- tables from myapp

=======================================================================================================

-------------------------------
5. How Django uses db.sqlite3
-------------------------------

In settings.py, you’ll see:

.. code-block:: python

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
        }
    }

This tells Django:
    “Use SQLite, and store data in db.sqlite3.”
	
=======================================================================================================

----------------------------
6. How to view db.sqlite3
----------------------------

**Option 1:** Django shell

.. code-block:: bash 

    python manage.py dbshell

**Option 2:** SQLite GUI tools
	- DB Browser for SQLite
	- TablePlus
	- DBeaver

These tools let you:
	- Browse tables
	- View data
	- Run SQL queries

=======================================================================================================

--------------------------------
7. What db.sqlite3 is GOOD for
--------------------------------

    - ✅ Learning Django
    - ✅ Tutorials
    - ✅ Small projects
    - ✅ Local development

=======================================================================================================

-------------------------------------
8. What db.sqlite3 is NOT good for
-------------------------------------

    - ❌ Production websites
    - ❌ Multiple concurrent users
    - ❌ High traffic
    - ❌ Large datasets

In production, Django commonly uses:
	- PostgreSQL
	- MySQL

=======================================================================================================

-------------------------------------------
9. Should db.sqlite3 be committed to Git?
-------------------------------------------

**Usually: NO**

Add this to your project-level .gitignore:

.. code-block:: bash 

    db.sqlite3

Why?
	- Contains local data
	- Machine-specific
	- Changes frequently

=======================================================================================================

--------------------------------------------
10. What happens if you delete db.sqlite3?
--------------------------------------------

If you delete it:
	- All data is lost
	- Django can recreate it

To recreate:

.. code-block:: bash 

    python manage.py migrate

Then optionally:

.. code-block:: bash 

    python manage.py createsuperuser

=======================================================================================================

Common beginner mistakes
	- Editing db.sqlite3 manually
	- Committing it to GitHub
	- Using it in production
	- Expecting it to sync across machines



