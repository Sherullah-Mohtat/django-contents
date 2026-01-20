bin 
====

---------------------------------
📂 djenv/bin — what it really is
---------------------------------

djenv/bin contains the Python interpreter, pip, Django commands, and activation scripts that make the virtual environment work.

**bin/ is the “control room” of the virtual environment.**

Everything that makes the venv work lives here:
	- Python executables
	- pip
	- Django commands
	- activation scripts

When you activate the venv, your system starts using **these files instead of global ones.**

===========================================================================================================================================

-------------------------
The most important idea
-------------------------

When you run:

.. code-block:: bash 

    source djenv/bin/activate

You are saying:
    “From now on, use **everything inside djenv/bin.**”

That’s it.

Nothing else in the system matters while it’s active.

**activate**

Used by:

.. code-block:: bash 

    source djenv/bin/activate

- Written for bash / zsh (macOS, Linux)
- Modifies:
- PATH
- Shell prompt
- Environment variables

After activation:

.. code-block:: bash 

    which python
    # → djenv/bin/python

This file is **why the venv works.**


