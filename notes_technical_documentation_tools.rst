##########################################
Notes on how to create technical documents
##########################################

restructuredText (reST, rST)
############################

- reStructuredText may provide the best tool as an accessible, flexible, readable, plain text, python based technical documentation option. reST is the source format, Sphinx is a builder tool that transforms reStructuredText into different target output formats.

- It can be integrated with Sphinx for converting to html, pdf, etc. and for supporting multiple languages (not just Python).

- reStructuredText is similar to Markdown. If webpages are the main objective maybe use Markdown though. 
For technical documents maybe reStructuredText is better. 

- reStructuredText seems much easier than html and LaTex and travels much better as it is plain text and can be used as the source for later conversion.

- With python+docutils+sphinx it can be formatted to html, with pdflatex to pdf for example.

- reStructuredText can be transfomed to Markdown with Pandoc and then rendered as html.

- reStructuredText supports math

- A good option is CGATReport, based on Python, Sphinx and rST. It integrates plotting code directly into its workflow though (good?). The central datastructure is a pandas dataframe. Has a table renderer.

- Also see Jupyter ecosystem and its notebook (previously IPython Notebook):
    http://jupyter.org/
    
    + This works well, looks great, has huge flexibility, is becoming language independent, great when run interactively.
    + Requires windowing though for the notebook which can be very cumbersome when working remotely.
    + Some problems when turning from notebook to script for automated analysis? 


Including citations
###################

- There are extensions for Mendeley and BibTex for citations. Mendeley Python:
    + http://mendeley-python.readthedocs.io/en/stable/
    + http://emilien.tlapale.com/bibgen/doc/source/rest.html
    + https://github.com/etlapale/bibgen

- See the Sphinx BibTeX extension:
    http://build-me-the-docs-please.readthedocs.io/en/latest/Using_Sphinx/UsingBibTeXCitationsInSphinx.html
    This is in beta though. 

    + BibTeX is the file format for jabref, a citation manager:
        * http://www.bibtex.org/
        * http://www.jabref.org/

- Mendeley looks good but is now owned by Elsevier, JabRef looks like a good open source option:
    + http://www.jabref.org/
    + https://en.wikipedia.org/wiki/JabRef
    It can import Endnote, might work with Word. It can export for Endnote format. Limited reference formats though. 

- Endnote can export to bibtex. The bibtex file can then be used as th einput for the rST directive.


reST directives to include external files
#########################################

- The subdocument and include directives in reStructuredText can include external files.
    + http://docutils.sourceforge.net/sandbox/package-doc/multiple-input-files.html#id6
    + http://reinout.vanrees.org/weblog/2010/12/08/include-external-in-sphinx.html


To include images
#################

Images can be pulled in with e.g.:
   ```.. image:: /path/to/image.jpg```


Making slide with rst
#####################

- A few references for writing slides with rst which can then be converted to PDF:
    http://rst2html5slides.readthedocs.io/en/latest/
    


Problems with reST
##################

- Tracking changes is a problem though (between collaborators not using git, i.e. collaborator's comments in a Word review form):
    http://criticmarkup.com/

- Rendering external tables easily with rST? See CGATReport and R library xtable

These aren't specific to rST though.


reST example sheet
##################
http://docutils.sourceforge.net/docs/user/rst/demo.txt


Miscellaneous
#############

- Pandoc is a universal document converter, it can do rST to ODT (for Word for example):
    http://pandoc.org/
    http://ralsina.me/stories/BBS52.html
    
    | and back (untested, probably not great if it has complex reviewer changes, logos, styles, etc.):
    https://peintinger.com/?p=365
    https://ronn-bundgaard.dk/blog/convert-docx-to-markdown-with-pandoc/
    https://www.tummy.com/blogs/2011/11/28/word-doc-authoring-with-pandoc/
    http://stackoverflow.com/questions/14249811/markdown-to-docx-including-complex-template

- R Markdown:
    + http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html
    + https://nicercode.github.io/guides/reports/

- R with rST and docutils and then conversion to any format (including ODT that can be opened with Word):
    + https://www.r-project.org/conferences/useR-2010/abstracts/Dasgupta.pdf
    + Examples, e.g. knitr for R with rst:
        * https://yihui.name/knitr/demo/minimal/
        * Input of R script for rST: https://github.com/yihui/knitr-examples/blob/master/006-minimal.Rrst
        * Output of the above: https://github.com/yihui/knitr-examples/blob/master/006-minimal.rst
        * http://www.agapow.net/science/data-science/writing-knitr-in-restructured-text/

The downside is that these formats then don't easily (?) allow to run the code as a script from the command line:
    + http://stackoverflow.com/questions/21512918/how-to-use-knitr-from-command-line-with-rscript-and-command-line-argument

Jupyter notebooks
#################

For exploratory analysis these_ might be a great solution. They are very flexible, can mix languages, keep plots, code, text together. See an example of a publication of RNA-seq here_ and a blog_ with some tips and info. A notebook server_ is needed to run properly. 

.. _these: https://jupyter.readthedocs.io/en/latest/index.html

.. _here: http://nbviewer.jupyter.org/github/maayanlab/Zika-RNAseq-Pipeline/blob/master/Zika.ipynb

.. _blog: http://blog.juliusschulz.de/blog/ultimate-ipython-notebook

.. _server: http://jupyter-notebook.readthedocs.io/en/latest/public_server.html


R markdown and its notebook
###########################

R markdown_ v2 is another excellent option in this regard. See also R Markdown to Word_. If you're running analysis locally, R notebooks and Jupyter are probably far better than rst and Sphinx for reports. See these blogs (a_, b_, c_, d_, e_) comparing R and Jupyter notebooks for instance and other tutorials. 

You can also run Rmd files with command line parameters like (f_, g_, h_). This is the main tutorial_.

Check the reference_ guide and article templates_ for Rmarkdown.

.. _a: https://www.r-bloggers.com/jupyter-and-r-markdown-notebooks-with-r/

.. _b: https://www.datacamp.com/community/blog/jupyter-notebook-r#gs.b5ENsjE

.. _c: https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook#gs.6r5cYnQ

.. _d: http://danielphadley.com/Jupyter-to-Rmarkdown/

.. _e: https://blog.rstudio.org/2016/10/05/r-notebooks/

.. _markdown: http://rmarkdown.rstudio.com/index.html

.. _Word: http://rmarkdown.rstudio.com/articles_docx.html

.. _f: http://stackoverflow.com/questions/31463143/pass-parameters-from-command-line-into-r-markdown-document

.. _g: http://stackoverflow.com/questions/32479130/passing-parameters-to-r-markdown?rq=1

.. _h: http://stackoverflow.com/questions/31822873/proper-r-markdown-code-organization?rq=1

.. _tutorial: http://rmarkdown.rstudio.com/lesson-1.html

.. _reference: https://github.com/rstudio/rticles

.. _templates: https://github.com/rstudio/rticles

VIM or Emacs?
#############

See org mode in vim_ for example (originally emacs).

.. _vim: http://www.vim.org/scripts/script.php?script_id=3642

TO DO
#####

.. note:: 

- Current thoughts:
    + Keep code, data and reports separate. 
    + Use rST for automatic reports run after pipeline analysis which could output plots, database, results table, methods, legends, etc.
    + Include generic narrative and pull in plots, tables, legends and methods text from external files (generated by the plot script or as text output from a given analysis).
    + Create meta rST to pull in automated reports and add ad hoc interpretation.


- How to include code (or reference to location) in the report?
- How to include parameters run, date, author, location, etc.?

- Check how to import tables, with CGATReport for example:
    + https://github.com/AndreasHeger/CGATReport/blob/master/doc/GalleryTables.rst

- And examples of reports:
    + https://www.cgat.org/downloads/qbh6mmrDkX/analysis_fdr0.01_report/pipeline/Methods.html#irf5-motifs
    + https://github.com/AndreasHeger/CGATReport/blob/master/doc/UseCase.rst

- See David M. use of R library to format for latex with e.g.:
    (from SwIMA_v1.0.1.Rnw ; http://web.bioinformatics.cicbiogune.es/swima/
    library(xtable)
    xtable(samples[,1:2], caption="Groups and their samples.", label="groups")
    xtable(contrasts, caption="Comparisons between groups.", label="comps")

- Similar to xtable is:
    https://www.rforge.net/doc/packages/knitr/kable.html

- Check examples of directory structure and source rst files to build a meta-report:
    + /ifs/projects/proj008/web/pipeline_proj008_meta_report/_static and /_sources
    + https://www.cgat.org/downloads/qbh6mmrDkX/analysis_fdr0.01_report/contents.html
    
- Check Jupyter ecosystem as this solves many of the issues above.


Some references and blogs
#########################

| https://github.com/kiith-sa/RestructuredText-tutorial


| http://openalea.gforge.inria.fr/doc/openalea/doc/_build/html/source/sphinx/rest_syntax.html#restructured-text-rest-and-sphinx-cheatsheet


| http://www.sphinx-doc.org/en/1.5.1/tutorial.html
| First Steps with Sphinx — Sphinx 1.5.1 documentation


| reStructuredText Primer
| http://www.sphinx-doc.org/en/1.5.1/rest.html#


| rst-cheatsheet.rst
| https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst


| http://docutils.sourceforge.net/docs/user/rst/quickref.html#hyperlink-targets


| DocOnce may also be an option, looks nice:
| http://hplgit.github.io/doconce/doc/pub/slides/scientific_writing-1.html
| http://hplgit.github.io/doconce/doc/web/index.html
| http://hplgit.github.io/teamods/writing_reports/


| Blogs with comparisons:
| https://opensource.com/life/15/8/markup-lowdown
| http://hyperpolyglot.org/lightweight-markup


| http://zverovich.net/2016/06/16/rst-vs-markdown.html
| reStructuredText vs Markdown for documentation


| https://www.pydanny.com/markup-language-faceoff-lists.html
| Markup Language Faceoff: Lists


| https://varnish-cache.org/docs/2.1/phk/sphinx.html
| Why Sphinx and reStructuredText ? — Varnish version 2.1.5 documentation


| http://build-me-the-docs-please.readthedocs.io/en/latest/Using_Sphinx/UsingBibTeXCitationsInSphinx.html
| Managing bibliographic citations in Sphinx — Wiser 0.1 documentation


| https://en.wikipedia.org/wiki/ReStructuredText
| reStructuredText - Wikipedia


| https://www.mendeley.com/reference-management/reference-manager
| Reference Manager | Mendeley


| https://en.wikipedia.org/wiki/Comparison_of_document_markup_languages


| Writing Scientific Papers Using Markdown
| https://danieljhocking.wordpress.com/2014/12/09/writing-scientific-papers-using-markdown/


| How To Write Papers with Restructured Text 
| http://acooke.org/cute/HowToWrite1.html


| Standard format conversions between reST and LaTeX:
| http://goer.org/Journal/2011/01/publishing_with_sphinx_rest_and_sffms_latex.html


| Writing and publishing with Git and reST::
| https://jimmyg.org/blog/2009/my-experience-of-using-restructuredtext-to-write-the-definitive-guide-to-pylons.html


| There is some support for reST to Word::
| http://docutils.sourceforge.net/sandbox/rst2wordml/readme.html


| Sphinx tutorial::
| https://evolvingweb.ca/blog/writing-documentation-restructured-text-and-sphinx


| Reference manager comparison::
| https://en.wikipedia.org/wiki/Comparison_of_reference_management_software
