Creating figure layouts for publication programmatically
########################################################

It seems surprisingly hard to find tools for this. The current workflow I'd suggest (based on Python, essentially out of 
the `svgutils blog`_):

1. Plot with any tool, save as svg
2. Import figures you want into sgvutils
3. Create legends, titles, layout, etc.
4. Save multi-panel figure as svg

You can then:

5. Convert svg to pdf (with inkscape on the command line for example)
6. Insert images into rst with image and other directives to create a file with text, figures, tables, etc. and which can later be converted to pdf or html.

See below for details, references and basic examples. I haven't tested many of these but left them here as suggestions.

Python and svg
++++++++++++++

Python package svgutils_, probably the one to use, starts and ends with svg files.

`See this explanation`_ for more details.

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


A similar package is `svg_stack: concatenate SVG files`_

A useful svg utility package might be scour_.

.. _svgutils: https://github.com/btel/svg_utils

.. _`svgutils blog`: https://neuroscience.telenczuk.pl/?p=331

.. _`See this explanation`: http://svgutils.readthedocs.io/en/latest/tutorials/composing_multipanel_figures.html

.. _`svg_stack: concatenate SVG files`: https://github.com/astraw/svg_stack

.. _scour: https://github.com/scour-project/scour


Convert SVG to other formats
++++++++++++++++++++++++++++

Inkscape_

.. _Inkscape: https://inkscape.org/en/download/mac-os/

e.g.

.. code-block:: bash

    inkscape --file=fig_final.svg --export-area-drawing --without-gui --export-pdf=output.pdf

Full suite, equivalent to Adobe Illustrator but open source and free.

To install in Mac you can use:

.. code-block:: bash

    brew install caskformula/caskformula/inkscape

Another package for image file conversions is CairoSVG_.

.. _CairoSVG: http://cairosvg.org/

.. code-block:: bash
    
    cairosvg -o fig_final.pdf fig_final.svg


restructuredText and SVG
########################

See the documentation on `reStructuredText and svg`_. The mix of pdf, svg, rst, html, etc. can become nightmarish.

rst doesn't seem to have a specific figure layout tool but there are `some workarounds`_.

See the `image rst directive details`_ for more information and examples.

There is also the figure directive.

e.g. 

.. code-block::

    .. image:: _images/report_title.svg
       :width: 30%
    
    .. image:: _images/report_slide1.svg
       :width: 30%

    .. image:: _images/report_slide2.svg
        :width: 30%

    .. image:: picture.svg
       :scale: 100 %
       :alt: alternate text
       :align: right

Latex does not support svg, requiring first to convert svg files to pdf or eps. Inkscape can be used for this.

If you're using latex `see this document`_ for further help.

.. code-block:: bash

    inkscape -D -z --file=image.svg --export-pdf=image.pdf --export-latex

There is a `Sphinx svg image directive`_ that you can try:

.. _`Sphinx svg image directive`: http://docutils-ext.readthedocs.io/en/latest/svgt.html


Tables are a different matter altogether. You can `wrap figures in a table within rst`_.

.. _`wrap figures in a table within rst`: http://stackoverflow.com/questions/12148428/rest-image-grid-with-captions?noredirect=1&lq=1

.. _`reStructuredText and svg`: http://docutils.sourceforge.net/test/functional/expected/standalone_rst_html4css1.html#svg-images

.. _`some workarounds`: http://stackoverflow.com/questions/10219634/image-grid-in-restructuredtext-sphinx/10229407#10229407

.. _`image rst directive details`: http://docutils.sourceforge.net/docs/ref/rst/directives.html#images

.. _`see this document`: http://mirrors.concertpass.com/tex-archive/info/svg-inkscape/InkscapePDFLaTeX.pdf


With R
++++++

grImport_ does something similar and can manipulate figures/images starting from PostScript:

.. _grImport: https://cran.r-project.org/web/packages/grImport/vignettes/import.pdf

Use imager_ (also here__) package which can import vector graphics, but is meant for image manipulation not creating layouts.

.. __: http://dahtah.github.io/imager/gimptools.html

.. _imager: http://dahtah.github.io/imager/


`Create and format PowerPoint documents from R software - Easy Guides - Wiki - STHDA`_

.. _`Create and format PowerPoint documents from R software - Easy Guides - Wiki - STHDA`: http://www.sthda.com/english/wiki/create-and-format-powerpoint-documents-from-r-software#add-plots-and-images


`Microsoft Word and PowerPoint Documents Generation ReporteRs package`_

.. _`Microsoft Word and PowerPoint Documents Generation ReporteRs package`: http://davidgohel.github.io/ReporteRs/index.html


`CRAN - Package cowplot`_

.. _`CRAN - Package cowplot`: https://cran.r-project.org/web/packages/cowplot/index.html


`Arranging plots in a grid`_

.. _`Arranging plots in a grid`: https://cran.r-project.org/web/packages/cowplot/vignettes/plot_grid.html

`CMBX12 - import.pdf`_

.. _`CMBX12 - import.pdf`: https://cran.r-project.org/web/packages/grImport/vignettes/import.pdf


Python image manipulators
+++++++++++++++++++++++++

OpenCV_

.. _OpenCV: https://opencv-python-tutroals.readthedocs.io/en/latest/#

`PIL Pillow Fork`_

.. _`PIL Pillow Fork`: https://pillow.readthedocs.io/en/4.0.x/

Both are for statistical image processing


Other references
++++++++++++++++

`How to Create Publication-Quality Figures`_

.. _`How to Create Publication-Quality Figures`: http://cellbio.emory.edu/bnanes/figures/#414


`Overview Inkscape`_

.. _`Overview Inkscape`: https://inkscape.org/en/about/overview/


`Ten Simple Rules for Better Figures`_

.. _`Ten Simple Rules for Better Figures`: http://journals.plos.org/ploscompbiol/article/file?id=10.1371/journal.pcbi.1003833&type=printable


`imagemagick - How can I convert a PNG to a PDF in high quality so it's not blurry or fuzzy? - Unix & Linux Stack Exchange`_

.. _`imagemagick - How can I convert a PNG to a PDF in high quality so it's not blurry or fuzzy? - Unix & Linux Stack Exchange`: http://unix.stackexchange.com/questions/42856/how-can-i-convert-a-png-to-a-pdf-in-high-quality-so-its-not-blurry-or-fuzzy


`Combine several images horizontally with Python - Stack Overflow`_

.. _`Combine several images horizontally with Python - Stack Overflow`: http://stackoverflow.com/questions/30227466/combine-several-images-horizontally-with-python


`Python Image Library: How to combine 4 images into a 2 x 2 grid? - Stack Overflow`_

.. _`Python Image Library: How to combine 4 images into a 2 x 2 grid? - Stack Overflow`: http://stackoverflow.com/questions/4567409/python-image-library-how-to-combine-4-images-into-a-2-x-2-grid
