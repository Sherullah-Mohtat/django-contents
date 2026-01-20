pyvenv.cfg 
============

What is pyvenv.cfg?

pyvenv.cfg is a configuration file that describes how the virtual environment was created.

It tells Python:
	•	Which **base Python** was used
	•	Whether **system packages** are visible
	•	What **Python version** this venv uses

Python reads this file **automatically** when the venv’s python starts.

==============================================================================================

**Where it lives**

In your project:

.. code-block:: bash 

    django_project/
    └── djenv/
        └── pyvenv.cfg   ← here

It belongs **only** to the virtual environment.

==============================================================================================

**Typical contents of pyvenv.cfg**

Open it and you’ll see something like:

.. code-block:: bash 

    home = /usr/bin/python3.14
    include-system-site-packages = false
    version = 3.14.0

Let’s explain **each line.**

==============================================================================================

**1️⃣ home = ...**

Example:

.. code-block:: bash 

    home = /usr/bin/python3.14

Meaning:
	- This is the **system Python** used to create the venv
	- The venv’s python is based on this interpreter

If you delete or change this Python, the venv breaks.

==============================================================================================

**2️⃣ include-system-site-packages = false**

This is very important.
	- false → venv is **isolated**
	- true → venv can see **global packages**

Best practice:

.. code-block:: bash 

    include-system-site-packages = false

That ensures:
	- No pollution from system Python
	- Fully reproducible environment

==============================================================================================

**3️⃣ version = 3.14.0**

This is the **Python version** used.

It is informational:
	- Helps tools
	- Helps IDEs
	- Helps debugging

==============================================================================================

**How Python uses pyvenv.cfg**

When you run:

.. code-block:: bash 

    djenv/bin/python

Python:
	1.	Reads pyvenv.cfg

	2.	Knows it’s in a venv

	3.	Adjusts sys.path

	4.	Loads packages from djenv/lib/...

You never have to do this manually.

❌ What NOT to do with pyvenv.cfg
	- ❌ Don’t edit it manually
	- ❌ Don’t commit it to Git
	- ❌ Don’t copy it between projects

If something is wrong → recreate the venv.

==============================================================================================

**When does this file change?**

Only when:
	- You recreate the venv
	- You use a different Python version
	- You change system Python

Installing packages does **not** change this file.

Analogy
	- 🧾 pyvenv.cfg = birth certificate of the venv
	- 🐍 bin/python = the actual Python
	- 📦 lib/ = installed packages

