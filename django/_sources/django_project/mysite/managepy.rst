manage.py
===========

---------------------------
**1. What is manage.py?**
---------------------------

manage.py is the command-line interface for a Django project. It sets the project’s settings module and allows developers to execute administrative tasks such as running the development server, creating applications, and managing database migrations.

It is the **main entry point** you use to:
	- run the development server
	- create apps
	- manage the database
	- perform administrative tasks

Location:

.. code-block:: bash 

    mysite/manage.py

=================================================================================================

-----------------------------------
**2. Why does manage.py exist?**
-----------------------------------

Django needs two things to run commands correctly:
	#.	To know which settings file to use
	#.	To pass your command (like runserver) into Django’s internal system

manage.py does exactly that.

Think of it as a bridge between your terminal and Django.

=================================================================================================

-----------------------------
**3.How you use manage.py**
-----------------------------

Almost every Django command starts like this:

.. code-block:: bash 

    python manage.py <command>

If manage.py is missing or you run commands outside its folder, Django won’t work.

**Common examples**

.. code-block:: bash 

    python manage.py runserver
    python manage.py startapp blog
    python manage.py makemigrations
    python manage.py migrate
    python manage.py createsuperuser
    python manage.py shell

Check out `this list <../../tutorials/.managepy_commands.html>`_ for more commands.

=================================================================================================

--------------------------------------
**4. Typical contents of manage.py**
--------------------------------------

.. code-block:: python 

    #!/usr/bin/env python
    import os
    import sys

    def main():
        os.environ.setdefault(
            'DJANGO_SETTINGS_MODULE',
            'mysite.settings'
        )
        try:
            from django.core.management import execute_from_command_line
        except ImportError:
            raise
        execute_from_command_line(sys.argv)

    if __name__ == '__main__':
        main()

=================================================================================================

**1️⃣ Set the settings module**
---------------------------------

.. code-block:: python 

    os.environ.setdefault(
        'DJANGO_SETTINGS_MODULE',
        'mysite.settings'
    )

This tells Django:

“Use mysite/settings.py as the configuration file for this project.”

mysite.settings refers to the **inner mysite/ folder**, not the outer one.

=================================================================================================

**2️⃣ Import Django’s command system**
----------------------------------------

.. code-block:: python 

    from django.core.management import execute_from_command_line

This imports Django’s internal command handler.

All commands like runserver, migrate, etc. are implemented inside Django itself.

=================================================================================================

**3️⃣ Execute the command**
-----------------------------

.. code-block:: bash 

    execute_from_command_line(sys.argv)

This line:
	- Reads what you typed in the terminal
	- Passes it to Django
	- Executes the corresponding command

Example:

.. code-block:: bash 

    python manage.py runserver

sys.argv contains:

.. code-block:: python

    ["manage.py", "runserver"]

=================================================================================================

What manage.py is NOT
	- Not the web server
	- Not a settings file
	- Not an app
	- Not imported in your code

It is only a **launcher and dispatcher.**

=================================================================================================

**Why you should NOT modify manage.py**

In most projects:
	- manage.py stays unchanged
	- Django generates it correctly
	- Editing it can break commands

You only modify it in **advanced custom setups.**

=================================================================================================

Common beginner mistakes
	- Running Django commands outside the folder containing manage.py
	- Renaming manage.py
	- Deleting it accidentally
	- Thinking it runs automatically without the terminal

You avoided all of these 


