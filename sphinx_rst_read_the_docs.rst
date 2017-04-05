########################################################
How to generate python package documentation with Sphinx
########################################################


- Install Sphinx, sphinx-quickstart, sphinx-apidoc, sphinx-build

- In the python package docs directory that you would've created:
	+ Run 'sphinx-quickstart' to setup configuration values and generate template rst docs
	+ Manually edit index.rst and other files to use as content
	+ sphinx-apidoc -o . .. to generate module and function documents from docstrings within scripts
	+ make html to generate the first build
	+ sphinx-autobuild . _build_html
	+ Pull/push etc to GitHub account
	+ Create an account in ReadTheDocs and connect to GitHub repository
	+ Some configuration is needed (TO DO)
	+ RTD rebuilds after every commit using 'sphinx-build -b html . _build/html'
	+ If the build on RTD doesn't work try 'Wipe' in /projects/[project]/versions/



Links with more information:
http://docs.readthedocs.io/en/latest/builds.html
https://daler.github.io/sphinxdoc-test/includeme.html




