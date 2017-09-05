Creating figure layouts programmatically
########################################

With python and rst
+++++++++++++++++++

rst doesn't have a specific layout tool (?), `some workarounds`_

.. _`some workarounds`: http://stackoverflow.com/questions/10219634/image-grid-in-restructuredtext-sphinx/10229407#10229407

`Image rst directive details`_

.. _`Image rst directive details`: http://docutils.sourceforge.net/docs/ref/rst/directives.html#images

e.g. 

.. code-block::

	.. image:: _images/report_title.png
	   :width: 30%
	.. image:: _images/report_slide1.png
	   :width: 30%
	.. image:: _images/report_slide2.png
	   :width: 30%


`Wrap figures in a table within rst`_

.. _`Wrap figures in a table within rst`: http://stackoverflow.com/questions/12148428/rest-image-grid-with-captions?noredirect=1&lq=1


Python package svgutils_, probably the one to use, starts from SVG

.. _svgutils: https://github.com/btel/svg_utils

`See this explanation`_. 

.. _`See this explanation`: http://svgutils.readthedocs.io/en/latest/tutorials/composing_multipanel_figures.html

.. code-block:: python

    from svgutils.compose import *

    Figure("16cm", "6.5cm", 
            Panel(
                  SVG("sigmoid_fit.svg"),
                  Text("A", 25, 20, size=12, weight='bold')
                 ),
            Panel(
                  SVG("anscombe.svg").scale(0.5),
                  Text("B", 25, 20, size=12, weight='bold')
                 ).move(280, 0)
            ).save("fig_final_compose.svg")


With R
++++++

grImport_ does something similar and can manipulate figures/images starting from PostScript:

.. _grImport: https://cran.r-project.org/web/packages/grImport/vignettes/import.pdf

Use imager_ (also here__) package which can import vector graphics, but is meant for image manipulation not creating layouts.

.. __: http://dahtah.github.io/imager/gimptools.html

.. _imager: http://dahtah.github.io/imager/


Convert SVG to other formats
++++++++++++++++++++++++++++

CairoSVG_

.. _CairoSVG: http://cairosvg.org/

e.g.

.. code-block:: bash
    
    cairosvg -o fig_final.pdf fig_final.svg

Works well, python library, only converts

Inkscape_

.. _Inkscape: https://inkscape.org/en/download/mac-os/

e.g.

.. code-block:: bash

    inkscape --file=fig_final.svg --export-area-drawing --without-gui --export-pdf=output.pdf

Full suite though, equivalent to Adobe Illustrator

Use:

.. code-block:: bash

    brew install caskformula/caskformula/inkscape

to install version 0.92.1, this works well.

Python image manipulators
+++++++++++++++++++++++++

OpenCV

PIL Pillow Fork

Both are for statistical image processing

References to check
+++++++++++++++++++

`How to Create Publication-Quality Figures`_

.. _`How to Create Publication-Quality Figures`: http://cellbio.emory.edu/bnanes/figures/#414

https://inkscape.org/en/about/overview/
Overview | Inkscape
http://journals.plos.org/ploscompbiol/article/file?id=10.1371/journal.pcbi.1003833&type=printable
pcbi.1003833 1..7 - file
http://unix.stackexchange.com/questions/42856/how-can-i-convert-a-png-to-a-pdf-in-high-quality-so-its-not-blurry-or-fuzzy
imagemagick - How can I convert a PNG to a PDF in high quality so it's not blurry or fuzzy? - Unix & Linux Stack Exchange
http://dahtah.github.io/imager/gimptools.html
Imager as image editor
http://www.sthda.com/english/wiki/create-and-format-powerpoint-documents-from-r-software#add-plots-and-images
Create and format PowerPoint documents from R software - Easy Guides - Wiki - STHDA
http://davidgohel.github.io/ReporteRs/index.html
Microsoft Word and PowerPoint Documents Generation • ReporteRs package
https://github.com/btel/svg_utils
btel/svg_utils: Python tools to create and manipulate SVG files
https://cran.r-project.org/web/packages/cowplot/index.html
CRAN - Package cowplot
https://cran.r-project.org/web/packages/cowplot/vignettes/plot_grid.html
Arranging plots in a grid
http://docutils.sourceforge.net/docs/ref/rst/directives.html#images
reStructuredText Directives
https://cran.r-project.org/web/packages/grImport/vignettes/import.pdf
CMBX12 - import.pdf
http://stackoverflow.com/questions/30227466/combine-several-images-horizontally-with-python
Combine several images horizontally with Python - Stack Overflow
http://stackoverflow.com/questions/4567409/python-image-library-how-to-combine-4-images-into-a-2-x-2-grid
Python Image Library: How to combine 4 images into a 2 x 2 grid? - Stack Overflow
https://pillow.readthedocs.io/en/4.0.x/
Pillow — Pillow (PIL Fork) 4.0.0 documentation
https://opencv-python-tutroals.readthedocs.io/en/latest/#
Welcome to OpenCV-Python Tutorials’s documentation! — OpenCV-Python Tutorials 1 documentation
http://cairosvg.org/
CairoSVG
https://github.com/astraw/svg_stack
astraw/svg_stack: concatenate SVG files
https://www.r-bloggers.com/a-quick-exploration-of-the-reporters-package/
A quick exploration of the ReporteRs package | R-bloggers
