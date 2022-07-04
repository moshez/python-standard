Python Project Copier Template
==============================

This template produces a Python project.

Quickstart
----------

Initialize a project using
`copier`_
and
`nox`_:

.. code::

    $ copier gh:moshez/python-standard.git <TARGET_DIRECTORY>
    $ cd TARGET_DIRECTORY
    $ nox -e refresh_deps

**Note**:
Running
:code:`nox -e refresh_deps`
produces
:code:`requirements-*.txt`
files,
which are essential to the other sessions in
:code:`nox`.

.. _copier: https://copier.readthedocs.io/en/stable/

Working With the Project
------------------------

Testing
^^^^^^^

The configuration assumes you care about testing.
It uses
`virtue`_
to run the tests.

Since
`virtue`_
assumes tests are importable code,
put tests under your project:
:code:`PROJECT_NAME/tests/...`.
An example test is already included,
which checks the version number.


The
`virtue`_
runner
is only a runner:
it does not have test cases or assertions built in.
In order to write test cases,
use
:code:`unittest.TestCase`.
The
`hamcrest`_
library is already included in the test dependencies,
and can be used for writing assertions.

Managing dependencies
^^^^^^^^^^^^^^^^^^^^^

Add unpinned dependencies to
:code:`pyproject.toml`.
After doing that,
run

.. code::

    $ nox -e refresh_deps

This will recreate the pinned files.
Note that all other sessions only use the pinned files.

Pinning is useful:
a
:code:`nox`
session will not fail just because a new Python package has been uploaded to
PyPI.
However,
this does require periodic repinning.

There are services that will automatically suggest a patch for repinning.
If you do not use those,
you can create a branch yourself:

.. code::

    $ git checkout -b update-dependencies
    $ nox -e refresh_deps

Create a Pull Request/Merge Request
from the branch as you would for any other branch.

Releasing
^^^^^^^^^

The version number is managed in
:code:`pyproject.toml`.
There is no internal tool used to bump the version number.

Running
:code:`nox -e build`
or
:code:`nox`
will produce a wheel.
This wheel can be uploaded to a
Python packaging index of your choice.

Documenting
^^^^^^^^^^^

The documentation is set up to use
`sphinx`_.
It automatically ignores
Jupyter-created
temporary files,
to allow including notebooks in a natural way.

It suggests a quick start guide,
followed by an API reference.
Adding new sections is sometimes a good idea.

Continuous Integration
^^^^^^^^^^^^^^^^^^^^^^

The continuous integration configured is
GitHub Actions.
This is a relatively simple configuration.

It assumes that each interpreter,
on each operating system,
achieves full coverage.
It also runs the tests only on
Ubuntu.


Python Ecosystem Stack
----------------------

* Uses
  `nox`_
  as its checker runner.
* For packaging:

  * `build`_
    for building a wheel.
  * `pyproject.toml`_
    for declaring package metadata.
  * `setuptools`_
    as the build system.
  * `pip-compile`_
    for pinning dependencies.
* For tests:

  * `virtue`_
    as test runner.
  *  `hamcrest`_
    as assertion library.
  * `coverage`_
    for coverage testing.
    Coverage is set to fail below 100%.
    Explicitly mark untested code with
    :code:`# pragma: no coverage`.
* For static checking:

  * `black`_
    for automatically fixable errors.
  * `flake8`_
    for other issues.
  * `mypy`_
    for type checking.
* For documentation:

  * `sphinx`_
    to generate documents.
  * `sphinx-apidoc`_
    to render doc strings.
* For continuous integration:
  * `GitHub Actions`_

.. _nox: https://nox.thea.codes/en/stable/
.. _virtue: https://virtue.readthedocs.io/en/stable/
.. _hamcrest: https://pyhamcrest.readthedocs.io/en/stable/
.. _black: https://black.readthedocs.io/en/stable/
.. _flake8: https://flake8.pycqa.org/en/latest/
.. _coverage: https://coverage.readthedocs.io/en/stable/
.. _mypy: https://mypy.readthedocs.io/en/stable/
.. _pyproject.toml: https://pip.pypa.io/en/stable/reference/build-system/pyproject-toml/
.. _setuptools: https://setuptools.pypa.io/en/stable/index.html
.. _pip-compile: https://github.com/jazzband/pip-tools
.. _sphinx-apidoc: https://www.sphinx-doc.org/en/master/man/sphinx-apidoc.html
.. _GitHub Actions: https://github.com/features/actions
.. _sphinx: https://www.sphinx-doc.org/en/master/index.html
