edx-lint  |Travis|_
===================
.. |Travis| image:: https://travis-ci.org/edx/edx-lint.svg?branch=master
.. _Travis: https://travis-ci.org/edx/edx-lint

A collection of code quality tools:

- A few pylint plugins to check for quality issues pylint misses.

- A command-line tool to generate config files like pylintrc from a master
  file (part of edx_lint), and a repo-specific tweaks file.


Using edx_lint
--------------

The ``edx_lint`` command can generate config files from its own master file. Install
the package using ``pip``::

    $ pip install edx-lint

The ``write`` sub-command will write a config file based on the contents of the
edx_lint master file::

    $ edx_lint write pylintrc

The file written contains a hash of its contents, to detect subsequent editing.
``edx_lint`` will detect this when it next tries to write the file.  If editing
is detected, the edited file will be moved aside so it can be compared to the
newly written file.

Using lint-amnesty
------------------

The ``lint-amnesty`` command can be used to squash all existing pylint errors
in a codebase, so that from then the repository can maintain pylint-cleanliness.
Install the package using ``pip``::

    $ pip install edx-lint

The ``lint-amnesty`` command expects pylint errors in the ``--output-format=parseable``
format::

    $ pylint my.python.package --output-format=parseable | lint-amnesty

This will add comments for every existing pylint violation that look like::

    # pylint: disable=some-error  # lint-amnesty

It will also remove any existing suppressions that pylint flags as being ``useless-suppressions``.

Customizing edx_lint
--------------------
You can customize the resulting pylintrc file by creating a pylintrc_tweaks file in the
current directory before running the ``write`` sub-command.  It should contain only the
settings you want to override.

**Note:** If your project is not a Django project, you'll want to disable the django plugins with
your pylintrc_tweaks file::

    [MASTER]
    load-plugins = edx_lint.pylint


Developing edx_lint
-------------------

To run the tests::

    $ make requirements
    $ make test


License
-------

The code in this repository is licensed under Apache 2.0.  Please see
``LICENSE.txt`` for details.

How To Contribute
-----------------

Contributions are very welcome.

Please read `How To Contribute <https://github.com/edx/edx-platform/blob/master/CONTRIBUTING.rst>`_ for details.

Even though it was written with ``edx-platform`` in mind, the guidelines
should be followed for Open edX code in general.


Mailing List and IRC Channel
----------------------------

You can discuss this code on the `edx-code Google Group`__ or in the
``#edx-code`` IRC channel on Freenode.

__ https://groups.google.com/forum/#!forum/edx-code
