Call
====

.. image:: https://api.codacy.com/project/badge/Grade/91959f98ff34469884415e96ba2ff763    :target: https://www.codacy.com/app/solarliner/call?utm_source=gitlab.com&amp;utm_medium=referral&amp;utm_content=solarliner/call&amp;utm_campaign=Badge_Grade

Thread-based, JS-like asynchronous calls for Python. Works in both
Python 2.7 and Python 3.5+.

Install
-------

Release version:

.. code:: bash
	pip install call

Development version

.. code:: bash

    git clone https://gitlab.com/solarliner/call.git
    cd call
    # Activate virtualenv if needed
    python setup.py install

The library requires no other dependencies, and (will soon) support
Python's ``await`` keyword.

Use
---

Create a call:

.. code:: python

    def cb(resolve, reject):
        result = factorial(100)
        resolve(result)
        
    call = Call(cb)

Wrap a synchronous function in a Call:

.. code:: python
    call = Call.from_function(factorial, 10)

Chain calls with the ``then`` keyword

.. code:: python

    call = Call(cb).then(lambda val: print(val))

Catch errors:

.. code:: python

    call = Call(cb)\
        .then(lambda val: raise Exception())\
        .catch(lambda err: print('Whoops'))

Compose calls:

.. code:: python

    results = Call.all([Call(cb) for _ in range(10)])

Block thread until resolved (or raises on failure):

.. code:: python

    result = call.wait()

Wait for call to either resolve or reject. Note that it is not recommended to get the data directly, as it may be
``None``, which may or may not indicate that an error has occurred.

.. code:: python

    call.join()
    result = call.data  # Not recommended

Contribute
----------

The repository follows the ``git flow`` standards. Create a feature branch, then ask for a pull/merge request.

The main repository is on GitLab, however the GitHub mirror is functional and you should be able to ask for pull
requests. However, they will be processed in GitLab.