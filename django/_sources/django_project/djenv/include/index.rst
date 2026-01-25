include
==========

--------------------------------------
**📂 djenv/include — what is it?**
--------------------------------------

include/ contains C header files for Python and native extensions.

It exists so that **Python packages written in C/C++** can be compiled and linked correctly.

=======================================================================================================

**Simple explanation**

Most Python packages are **pure Python** → they don’t need include.

Some packages are **partly written in C** → they need:
	- Python header files
	- System headers

Those headers live in djenv/include.

========================================================================================================

-----------------------------------------------
**What you typically find inside include/**
-----------------------------------------------

Structure looks like:

.. code-block:: bash 

    djenv/include/
    └── python3.x/
        ├── Python.h
        ├── object.h
        ├── unicodeobject.h
        └── ...

These files define:
	- Python objects
	- Memory management
	- C-API interfaces

========================================================================================================

-----------------------------------------
**When is include/ actually used?**
-----------------------------------------

You will only “use” include/ indirectly when:
	- Installing packages like:
	- psycopg2
	- numpy
	- pandas
	- lxml
	- cryptography

During installation:

.. code-block:: bash 

    pip install psycopg2
    
pip may compile C code and link against headers from:

.. code-block:: bash 

    djenv/include/

**Do Django projects use include/ directly?**

No.
	- Django itself is pure Python
	- You never import from include
	- You never edit files here

Django just benefits indirectly if a dependency uses C.

What NOT to do
	- Don’t open or edit files here
	- Don’t import anything from include
	- Don’t delete individual files
	- Don’t commit this folder to Git

