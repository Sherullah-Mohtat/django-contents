signals.py 
==============

-----------------------------------------------
What does “Register signals” mean in Django?
-----------------------------------------------

Registering signals means connecting Django events (like save or delete) to custom functions that run automatically when those events occur.

First: What is a signal?
--------------------------

A signal is Django’s way of saying:
    “Something happened — do you want to react to it?”

Examples:
	- A model was **saved**
	- A model was **deleted**
	- A user **logged** in
	- A request **started** or **finished**

Django **emits a signal**, and your code can **listen** and **respond.**

=========================================================================================================================================

**Simple real-world analogy**

Think of a doorbell:
	- Someone presses the button → 🔔 (signal)
	- The bell rings
	- You hear it and respond

In Django:
	- Model saved → 🔔 signal sent
	- Your function hears it
	- Your function runs automatically

=========================================================================================================================================

**Common Django signals**

Some very common ones:

.. list-table::
    :header-rows: 1

    * - Signal
      - When it fires
    * - post_save
      - After a model is saved
    * - pre_save
      - Before a model is saved
    * - post_delete
      - After a model is deleted
    * - user_logged_in
      - When a user logs in
    * - request_started
      - When request starts

=========================================================================================================================================

What is registering a signal
---------------------------------

Registering a signal = telling Django:
    “When THIS signal happens, run THIS function.”

Without registration:
    - ❌ Django doesn’t know your function exists
    - ❌ Your signal code never runs

=========================================================================================================================================

**Basic signal example**

**1️⃣ Create a signal handler**

Create a file:

.. code-block:: bash 

    myapp/signals.py

.. code-block:: python 

    from django.db.models.signals import post_save
    from django.dispatch import receiver
    from .models import MyModel


    @receiver(post_save, sender=MyModel)
    def mymodel_created(sender, instance, created, **kwargs):
        if created:
            print("A new MyModel was created!")

This function:
	- Listens to post_save
	- Runs **after** MyModel is saved
	- Only runs when it’s newly created

=========================================================================================================================================

**2️⃣ Register the signal (VERY IMPORTANT)**

Django does **not auto-load** signals.py.

You must register it manually.

In apps.py:

.. code-block:: python 

    from django.apps import AppConfig

    class MyappConfig(AppConfig):
        default_auto_field = 'django.db.models.BigAutoField'
        name = 'myapp'

        def ready(self):
            import myapp.signals

This line **registers the signals:**

.. code-block:: python 

    import myapp.signals

=========================================================================================================================================

----------------------------------------
Why register signals inside ready()?
----------------------------------------

Because:
	- Django loads apps lazily
	- Models may not be ready at import time
	- ready() runs **after everything is loaded**

**This is the safest place** to register signals.

=========================================================================================================================================

----------------------------------------------
What happens if you don’t register signals?
----------------------------------------------

❌ Signal file exists

❌ Code is correct

❌ Django never imports it

➡️ **Signal never fires**

This is one of the **most common Django mistakes.**

=========================================================================================================================================

**Mental model**

Think like this:
	- signals.py = **Listeners**
	- ready() = **Plugging the listeners in**
	- No ready() = No sound 🔕

=========================================================================================================================================

----------------------------------------
Why not import signals in models.py?
----------------------------------------

Bad idea ❌

It can cause:
	- Circular imports
	- App loading issues
	- Hard-to-debug bugs

Best practice:
    ✅ Always register signals in apps.py → ready()

=========================================================================================================================================

-------------------------------
When should you use signals?
-------------------------------

Good use cases ✅:
	- Auto-create related objects (profile for user)
	- Logging activity
	- Sending notifications
	- Keeping models in sync

Bad use cases ❌:
	- Core business logic
	- Complex workflows
	- Things that must be explicit

=========================================================================================================================================

---------------------------------
Where to put signals in Django
---------------------------------

**Short answer (best practice)**

**Put signals in:**

.. code-block:: bash 

    myapp/signals.py

Register them in:

.. code-block:: bash 

    myapp/apps.py

This is the **official, clean, production-safe Django pattern.**

=========================================================================================================================================

**Recommended app structure**

.. code-block:: bash 

    myapp/
    ├── __init__.py
    ├── admin.py
    ├── apps.py        <-- register signals here
    ├── models.py
    ├── signals.py     <-- write signals here
    ├── tests.py
    ├── views.py
    ├── migrations/

=========================================================================================================================================

-------------------------------------
Why NOT put signals in other files?
-------------------------------------

Let’s go through common mistakes 

**❌ models.py (DON’T)**

.. code-block:: python 

    # BAD PRACTICE
    from django.db.models.signals import post_save

Why bad?
	- Circular imports
	- Models may not be ready
	- Hard-to-debug startup bugs

----------------------------------------------------------------------------------------------------------------------------------------

**❌ views.py (WRONG)**

Signals are:
	- Model-level events
	- System-level reactions

Views are:
	- HTTP request/response logic

🚫 Mixing these breaks separation of concerns.

----------------------------------------------------------------------------------------------------------------------------------------

**❌ __init__.py (NO)**

This file should stay **minimal.**

Signals here can cause:
	- App loading order issues
	- Hidden side effects

=========================================================================================================================================

**✅ Correct implementation (step by step)**

**1️⃣ Create signals.py**

.. code-block:: python 

    # myapp/signals.py
    from django.db.models.signals import post_save
    from django.dispatch import receiver
    from .models import MyModel


    @receiver(post_save, sender=MyModel)
    def mymodel_created(sender, instance, created, **kwargs):
        if created:
            print("MyModel created")

----------------------------------------------------------------------------------------------------------------------------------------

**2️⃣ Register signals in apps.py**

.. code-block:: python 

    # myapp/apps.py
    from django.apps import AppConfig


    class MyappConfig(AppConfig):
        default_auto_field = 'django.db.models.BigAutoField'
        name = 'myapp'

        def ready(self):
            import myapp.signals

This line **activates** your signals:

.. code-block:: python 

    import myapp.signals

----------------------------------------------------------------------------------------------------------------------------------------

**3️⃣ Ensure app config is used (IMPORTANT)**

In settings.py:

.. code-block:: python 

    INSTALLED_APPS = [
        'myapp.apps.MyappConfig',
    ]

✅ This ensures ready() runs

❌ 'myapp' alone may skip signal registration in some setups

----------------------------------------------------------------------------------------------------------------------------------------

Django does **not auto-load** signals.py.

You must:
	#.	Import it
	#.	At the right time
	#.	After apps + models are ready

That’s exactly what apps.py → ready() does.

Write signals in signals.py, register them in apps.py, never in models.py.

----------------------------------------------------------------------------------------------------------------------------------------

**Simple mental model**

.. list-table:: 
    :header-rows: 1

    * - File
      - Role
    * - signals.py
      - What should happen
    * - apps.py
      - When to activate
    * - ready()
      - Plug everything in



