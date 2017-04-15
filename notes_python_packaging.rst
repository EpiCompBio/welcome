Packaging in Python
===================

Use the structure provided by project_quickstart.py_ as a starting example.

.. _project_quickstart.py: https://github.com/AntonioJBT/project_quickstart

Edit MANIFEST.in, your INI file and setup.py files as necessary

Use check-manifest_ to detect errors in setup.py:

.. _check-manifest: https://pypi.python.org/pypi/check-manifest

.. Also: https://github.com/mgedmin/check-manifest

.. code-block:: bash
	
	pip install check-manifest

	cd ~/src/mygreatpackage

	check-manifest

Run:

.. code-block:: python

	python setup.py check
	python setup.py sdist bdist_wheel

Create an environment and test in a separate directory:

.. code-block:: bash

	cd .. ; mkdir test_package ; cd test_package

	conda create -n test_env python=3.6

	Install any dependencies needed with conda or pip

	source activate test_env

	git clone https://github.com/xxx/package_xxx.git

Install and test package:

.. code-block:: bash

	cd package_xxx

	python setup.py install

Then test the main script elsewhere, run a test example, etc.


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


This blog_ has a good explanation of how to carry out all of this with examples of MANIFEST.in and setup.py files.

.. _blog: https://hynek.me/articles/sharing-your-labor-of-love-pypi-quick-and-dirty/

It also has further information on how to use `PyPI's test server`_.

.. _`PyPI's test server`: https://testpypi.python.org/pypi


Further references:

https://the-hitchhikers-guide-to-packaging.readthedocs.io/en/latest/introduction.html

https://wiki.python.org/moin/Distutils/Tutorial

http://www.diveintopython3.net/packaging.html

https://blog.niteoweb.com/setuptools-run-custom-code-in-setup-py

http://stackoverflow.com/questions/774824/explain-python-entry-points

http://stackoverflow.com/questions/13307408/python-packaging-data-files-are-put-properly-in-tar-gz-file-but-are-not-install?rq=1









