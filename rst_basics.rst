restructuredText tutorials/info:

  - http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html

  - http://docutils.sourceforge.net/docs/user/rst/quickstart.html

  - https://github.com/kiith-sa/RestructuredText-tutorial

  - http://www.sphinx-doc.org/en/1.5.1/rest.html

  - Play around with the online editor which converts rst to html: http://rst.ninjs.org/

-----

rst can be used on its own and then converted to html, pdf etc with different tools.

Sphinx_ adds many useful tools and is based on rst, one of the main ones is to connect many files to a single hierarchy of documents. Sphinx also makes it easy to document your python based project.

.. _Sphinx: http://www.sphinx-doc.org/en/stable/tutorial.html

Generate the documentation with sphinx::

   pip install sphinx

A sphinx template report can be generated with::

   mkdir my_report_docs

   cd my_report_docs

   sphinx-quickstart

After adding content, you can generate html, pdf, etc. with::

   make html

The rendered file will be found in the ``_build`` directory.

-----

Include other rst files::

  .. toctree::
      :maxdepth: 2
      :numbered:
      :titlesonly:
      :glob:
      :hidden:

      intro.rst
      chapter1.rst
      chapter2.rst

See the toctree_ directive for full info.

.. _toctree: http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html#include-other-rst-files-with-the-toctree-directive

-----

It is also possible to include the literal contents of a file with::

  .. literalinclude:: filename
      :linenos:
      :language: python
      :lines: 1, 3-5
      :start-after: 3
      :end-before: 5

Include an image::

  .. image:: images/ball1.gif
  
  

Or::

  .. image:: images/xxx.png
     :height: 100
    :width: 200
    :scale: 50
    :alt: alternate text

See image_ directive full markup.

.. _image: http://docutils.sourceforge.net/docs/ref/rst/directives.html#images

Or import a figure which can have a caption and whatever else you add::

  .. figure:: xxx.jpg
      :width: 200px
      :align: center
      :height: 100px
      :alt: alternate text
      :figclass: align-center
      
      a caption would be written here as plain text. You can add more with eg::
  
    .. code-block:: python

        import image

-----

Include a simple csv table::

  .. csv-table:: a title
     :header: "name", "firstname", "age"
     :widths: 20, 20, 10
     
     "Smith", "John", 40
     "Smith", "John, Junior", 20

See csv-table_ directive for example.

.. _csv-table: http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html#the-csv-table-directive


-----

For useful extensions to rst and sphinx see this tutorial on extensions_:

.. _extensions: http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html#useful-extensions

In a sphinx conf.py file you can specify the extensions needed, e.g.::

  extensions = [-
    'easydev.copybutton',
    'sphinx.ext.autodoc',
    'sphinx.ext.autosummary',
    'sphinx.ext.coverage',
    'sphinx.ext.graphviz',
    'sphinx.ext.doctest',
    'sphinx.ext.intersphinx',
    'sphinx.ext.todo',
    'sphinx.ext.coverage',
    'sphinx.ext.pngmath',
    'sphinx.ext.ifconfig',
    'matplotlib.sphinxext.only_directives',
    'matplotlib.sphinxext.plot_directive',
 ]

-----

The math directive, e.g.::

  .. math::

      n_{\mathrm{offset}} = \sum_{k=0}^{N-1} s_k n_k

-----

TODO, it needs the conf.py file::

would produce:

.. math::

    n_{\mathrm{offset}} = \sum_{k=0}^{N-1} s_k n_k

-----

References, e.g. [CIT2002]_ are defined at the bottom of the page as::

  .. [CIT2002] A citation

and called with::

  [CIT2002]_

-----
