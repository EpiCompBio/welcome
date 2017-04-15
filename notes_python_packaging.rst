===================
Packaging in Python
===================

Python packaging has a messy history and isn't completely straightforward.

See these webpages first and follow their guidelines:

`python - Differences between distribute, distutils, setuptools and distutils2? - Stack Overflow`_

.. _`python - Differences between distribute, distutils, setuptools and distutils2? - Stack Overflow`: http://stackoverflow.com/questions/6344076/differences-between-distribute-distutils-setuptools-and-distutils2?noredirect=1&lq=1

`Python Packaging User Guide — Python Packaging User Guide documentation`_

.. _`Python Packaging User Guide — Python Packaging User Guide documentation`: https://packaging.python.org/


`pypa/sampleproject: A sample project that exists for PyPUG's "Tutorial on Packaging and Distributing Projects"`_

.. _`pypa/sampleproject: A sample project that exists for PyPUG's "Tutorial on Packaging and Distributing Projects"`: https://github.com/pypa/sampleproject

-----

You can also see other package examples (e.g. cryptography_) and the Python package sample_.

.. _cryptography: https://github.com/pyca/cryptography

.. _sample: https://github.com/pypa/sampleproject


You can also use the structure provided by project_quickstart.py_ as a starting point.

.. _project_quickstart.py: https://github.com/AntonioJBT/project_quickstart


-----

Workflow
========

Once you have the project file and directory structure:
Get the packages you need, e.g.

.. code-block:: bash

	pip install -U pip twine check-manifest setuptools


Create/edit MANIFEST.in and setup.py files as necessary (and possibly an INI file depending on how you've set things up).

Use `check-manifest`_ to detect errors in setup.py:

.. _`check-manifest`: https://pypi.python.org/pypi/check-manifest

.. code-block:: bash

	check-manifest

Run the following to test and create the discribution:

.. code-block::

	python setup.py check
	
	python setup.py sdist bdist_wheel


You can create an environment and test in a separate directory (using conda for example):

.. code-block:: bash

	cd .. ; mkdir test_package ; cd test_package

	conda create -n test_env python=3.6

Install any dependencies needed with conda or pip

.. code-block:: bash

	source activate test_env

	git clone https://github.com/xxx/package_xxx.git

Install and test package:

.. code-block:: bash

	cd package_xxx

	python setup.py install


Then test the main script elsewhere (you can create an entry point in setup.py), run a test example, etc.


If this is an actual package to share with others upload to PyPI:

See the instructions_ page for all the details.

.. _instructions: https://packaging.python.org/distributing/#uploading-your-project-to-pypi

- Register yourself at PyPI_ and create a ~/.pypirc file.

.. _PyPI: https://pypi.python.org/pypi?%3Aaction=register_form

- Register your package manually or with twine (see instructions above)

- Upload your package (requires twine_ for this example):

.. _twine: https://github.com/pypa/twine

.. code-block:: bash
	
	twine upload dist/*

The package should now be ready to install anywhere with:

.. code-block:: bash

	pip install package_xxx


-----

Further references:

This blog_ has an explanation of how to carry out all of this with examples of MANIFEST.in and setup.py files.

.. _blog: https://hynek.me/articles/sharing-your-labor-of-love-pypi-quick-and-dirty/

It also has further information on how to use `PyPI's test server`_.

.. _`PyPI's test server`: https://testpypi.python.org/pypi

Things changed a fair amount from python 2x to 3x so check whatever is the most recent information (see the links above for this).


https://the-hitchhikers-guide-to-packaging.readthedocs.io/en/latest/introduction.html

https://wiki.python.org/moin/Distutils/Tutorial

http://www.diveintopython3.net/packaging.html

https://blog.niteoweb.com/setuptools-run-custom-code-in-setup-py

http://stackoverflow.com/questions/774824/explain-python-entry-points

http://stackoverflow.com/questions/13307408/python-packaging-data-files-are-put-properly-in-tar-gz-file-but-are-not-install?rq=1
