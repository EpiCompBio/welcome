##########################################
Notes on how to create technical documents
##########################################

restructuredText (reST)
#######################

- reStructuredText may provide the best tool as an accessible, flexible, readable, plain text, python based technical documentation option. reST is the source format, Sphinx is a builder tool that transforms reStructuredText into different target output formats.

- It can be integrated with Sphinx for converting to html, pdf, etc. and for supporting multiple languages (not just Python).

- reStructuredText is similar to Markdown. If webpages are the main objective maybe use Markdown though. 
For technical documents maybe reStructuredText is better. 

- reStructuredText seems much easier than html and LaTex and travels much better as it is .txt and can be used as the source for later conversion.

- With python+docutils+sphinx it can be formatted to html, with pdflatex to pdf for example.

- reStructuredText can be transfomed to Markdown with Pandoc and then rendered as html.

- reStructuredText supports math

Including citations:
####################

- There are extensions for Mendeley and BibTex for citations. Mendeley Python:
    + http://mendeley-python.readthedocs.io/en/stable/
    + http://emilien.tlapale.com/bibgen/doc/source/rest.html
    + https://github.com/etlapale/bibgen

- See the Sphinx BibTeX extension:
| http://build-me-the-docs-please.readthedocs.io/en/latest/Using_Sphinx/UsingBibTeXCitationsInSphinx.html
| This is in beta though.
| BibTeX is the file format for jabref, a citation manager:
    - http://www.bibtex.org/
    - http://www.jabref.org/

- Mendeley looks good but is now owned by Elsevier, JabRef looks like a good open source option:
    + http://www.jabref.org/
    + https://en.wikipedia.org/wiki/JabRef
| It can import Endnote, might work with Word. It can export for Endnote format. Limited reference formats though. 


reST directives to include external files:
##########################################

- The subdocument and include directives in reStructuredText can include external files.
    + http://docutils.sourceforge.net/sandbox/package-doc/multiple-input-files.html#id6
    + http://reinout.vanrees.org/weblog/2010/12/08/include-external-in-sphinx.html


To include images:
##################

Images can be pulled in with e.g.:

.. image:: /path/to/image.jpg


Problems with reST
##################

- Tracking changes is a problem though (between collaborators not using git):
http://criticmarkup.com/

- Rendering external tables? See CGATReport and R library xtable

reST example sheet
##################
http://docutils.sourceforge.net/docs/user/rst/demo.txt

Miscellaneous
#############

- Pandoc is a universal document converter:
http://pandoc.org/

- R Markdown:
http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html

TO DO:
######

- Check how to import tables, with CGATReport for example:
    + https://github.com/AndreasHeger/CGATReport/blob/master/doc/GalleryTables.rst

- And examples of reports:
    + https://www.cgat.org/downloads/qbh6mmrDkX/analysis_fdr0.01_report/pipeline/Methods.html#irf5-motifs
    + https://github.com/AndreasHeger/CGATReport/blob/master/doc/UseCase.rst

- See David M. use of R library to format for latex with e.g.:
    | (from SwIMA_v1.0.1.Rnw ; http://web.bioinformatics.cicbiogune.es/swima/
    | library(xtable)
    | xtable(samples[,1:2], caption="Groups and their samples.", label="groups")
    | xtable(contrasts, caption="Comparisons between groups.", label="comps")


Some references and blogs:
##########################

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


| Writing and publishing with Git and reST:
| https://jimmyg.org/blog/2009/my-experience-of-using-restructuredtext-to-write-the-definitive-guide-to-pylons.html


| There is some support for reST to Word:
| http://docutils.sourceforge.net/sandbox/rst2wordml/readme.html


| Sphinx tutorial:
| https://evolvingweb.ca/blog/writing-documentation-restructured-text-and-sphinx


| Reference manager comparison:
| https://en.wikipedia.org/wiki/Comparison_of_reference_management_software
