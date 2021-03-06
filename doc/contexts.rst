.. Licensed under the Apache License: http://www.apache.org/licenses/LICENSE-2.0
.. For details: https://github.com/nedbat/coveragepy/blob/master/NOTICE.txt

.. _contexts:

====================
Measurement contexts
====================

.. :history: 20180921T085400, new for 5.0

.. versionadded:: 5.0

Coverage.py measures whether code was run, but it can also record the context
in which it was run.  This can provide more information to help you understand
the behavior of your tests.

There are two kinds of context: static and dynamic.  Static contexts are fixed
for an entire run, and are set explicitly with an option.  Dynamic contexts
change over the course of a single run.


Static contexts
---------------

A static context is set by an option when you run coverage.py.  The value is
fixed for the duration of a run.  They can be any text you like, for example,
"python3" or "with_numpy".  The context is recorded with the data.

When you :ref:`combine multiple data files <cmd_combining>` together, they can
have differing contexts.  All of the information is retained, so that the
different contexts are correctly recorded in the combined file.

A static context is specified with the ``--context=CONTEXT`` option to
:ref:`the coverage run command <cmd_run>`, or the ``[run] context`` setting in
the configuration file.


Dynamic contexts
----------------

Dynamic contexts are found during execution.  They started from the question,
"what test ran this line?," but have been generalized to allow any kind of
context tracking.  As execution proceeds, the dynamic context changes
to record the context of execution.  Separate data is recorded for each
context, so that it can be analyzed later.

There are two ways to enable dynamic contexts:

* you can set the ``[run] dynamic_context`` option in your .coveragerc file, or

* you can enable a :ref:`dynamic context switcher <dynamic_context_plugins>`
  plugin.

The ``[run] dynamic_context`` setting has only one option now.  Set it to
``test_function`` to start a new dynamic context for every test function::

    [run]
    dynamic_context = test_function

Each test function you run will be considered a separate dynamic context, and
coverage data will be segregated for each.  A test function is any function
whose names starts with "test".

Ideas are welcome for other dynamic contexts that would be useful.


Context reporting
-----------------

There is currently no support for using contexts during reporting.  I'm
interested to `hear your ideas`__ for what would be useful.

__  https://nedbatchelder.com/site/aboutned.html
