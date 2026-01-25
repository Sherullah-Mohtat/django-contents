__init__.py
==============

------------------------------
**1. What is __init__.py?**
------------------------------

__init__.py tells Python that this directory is a package.

Location:

.. code-block:: bash 

    mysite/mysite/__init__.py

Without this file, Python would treat the folder as a normal directory, **not** as an importable module.

================================================================================================================

-------------------------------------------
**2. Why does Django need __init__.py?**
-------------------------------------------

Django imports your project like this:

.. code-block:: python 

    import mysite.settings
    import mysite.urls

That only works if:
	- mysite/ is a **Python package**
	- And Python packages require __init__.py

So this file enables **imports.**

================================================================================================================

--------------------------------------
**3. What is inside __init__.py?**
--------------------------------------

By default:

.. code-block:: python 

    # empty

Yes — **empty on purpose.**

Its presence matters more than its content.

================================================================================================================

--------------------------------------------------
**4. What happens if you delete __init__.py?**
--------------------------------------------------

- Django will fail
- Imports will break
- Errors like:

.. code-block:: bash 

    ModuleNotFoundError: No module named 'mysite'

This is why Django always creates it.

================================================================================================================

**Does Django execute __init__.py?**

Yes — but only when the package is imported.

However:
	- Since it’s empty, nothing happens
	- No performance cost
	- No side effects

================================================================================================================

**Can we put code inside __init__.py?**

Yes, but rarely recommended.

Possible (advanced use cases):

.. code-block:: python 

    default_app_config = "mysite.apps.MySiteConfig"

Or exposing shortcuts:

.. code-block:: python 

    from .settings import BASE_DIR

For beginners and most projects:

**Leave it empty**

================================================================================================================

**Why every app also has __init__.py**

You’ll notice:

.. code-block:: bash 

    myapp/__init__.py
    mysite/__init__.py

Reason:
	- Apps are Python packages
	- Django imports them
	- Same rule applies everywhere







