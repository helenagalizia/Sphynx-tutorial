Concurrency and async / await
=============================

Details about the ``async def`` syntax for path operation functions and some background about asynchronous code, concurrency, and parallelism.

In a Hurry?
***********

If you are using third party libraries that tell you to call them with ``await``, like:

.. code-block:: python

    results = await some_library()

Then, declare your path operation functions with ``async def`` like:

.. code-block:: python

    @app.get('/')
    async def read_results():
        results = await some_library()
        return results

.. note::

    You can only use ``await`` inside of functions created with ``async def``.

------------------------------------------------------------------------------------

If you are using a third party library that communicates with something (a database, an API, the file system, etc.) 
and doesn't have support for using ``await``, (this is currently the case for most database libraries), 
then declare your path operation functions as normally, with just ``def``, like:

.. code-block:: python

    @app.get('/')
    def results():
        results = some_library()
        return results

----------------

If your application (somehow) doesn't have to communicate with anything else and wait for it to respond, use ``async def``.

------------

If you just don't know, use normal ``def``.

--------------

Note: You can mix ``def`` and ``async def`` in your path operation functions as much as you need and define each one using the best option for you. 
FastAPI will do the right thing with them.

Anyway, in any of the cases above, FastAPI will still work asynchronously and be extremely fast.

But by following the steps above, it will be able to do some performance optimizations.

Technical Details
*****************

Modern versions of Python have support for **"asynchronous code"** using something called "coroutines", with ``async`` and ``await`` syntax.

Let's see that phrase by parts in the sections below:

* **Asynchronous Code**
* ``async`` and ``await``
* **Coroutines**

Asynchronous Code
*****************

Concurrent Burgers
++++++++++++++++++

You go with your crush to get fast food, you stand in line while the cashier takes the orders from the people in front of you. 😍

.. image:: https://fastapi.tiangolo.com/img/async/concurrent-burgers/concurrent-burgers-01.png

Then it's your turn, you place your order of 2 very fancy burgers for your crush and you. 🍔🍔

.. image:: https://fastapi.tiangolo.com/img/async/concurrent-burgers/concurrent-burgers-02.png

The cashier says something to the cook in the kitchen so they know they have to prepare your burgers
(even though they are currently preparing the ones for the previous clients).

.. image:: https://fastapi.tiangolo.com/img/async/concurrent-burgers/concurrent-burgers-03.png

You pay. 💸

The cashier gives you the number of your turn.

.. image:: https://fastapi.tiangolo.com/img/async/concurrent-burgers/concurrent-burgers-04.png

While you are waiting, you go with your crush and pick a table, you sit and talk with your crush for a long time
(as your burgers are very fancy and take some time to prepare).

As you are sitting at the table with your crush, while you wait for the burgers, 
you can spend that time admiring how awesome, cute and smart your crush is ✨😍✨.

.. image:: ./_static/burger3.png

While waiting and talking to your crush, from time to time, you check the number displayed on the counter to see if it's your turn already.

Then at some point, it finally is your turn. You go to the counter, get your burgers and come back to the table.

.. tip::

    Beautiful illustrations by `Ketrina Thompson <https://www.instagram.com/ketrinadrawsalot/>`_. 🎨

-------------

Conclusion
**********

Let's see the same phrase from above:

    Modern versions of Python have support for **"asynchronous code"** using something called **"coroutines"**, with ``async`` and ``await`` syntax.

That should make more sense now. ✨

All that is what powers FastAPI (through Starlette) and what makes it have such an impressive performance

Very Technical Details
**********************

.. warning::

    You can probably skip this.

    These are very technical details of how **FastAPI** works underneath.

    If you have quite some technical knowledge (co-routines, threads, blocking, etc.) and are curious about how FastAPI handles ``async def`` vs normal ``def``, go ahead.


