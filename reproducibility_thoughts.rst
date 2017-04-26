###############################################
Notes on reproducibility in biomedical research
###############################################

:Author: Antonio
:Date: 22 Dec 2016



General approach
################

The core idea is about reproducibility, integrating best practice, creating good habits and learning together. Reproducibility is the key principle. This (simply but not easily) requires discipline and a few tools that can be used and/or understood by as many people as possible.

Our research needs to be:

+ Reproducible (same question, same data, same code, same results)
+ Replicable (by other labs using other experiments, data, analysis, technology, etc.)
+ And ideally open source, open access and open data with code that is re-usable (by us and others)

The above requires:

+ Clear questions and hypotheses
+ Accessible, read-only data (data collection and experiments largely already follow these guidelines but the same applies)
+ Transparent, easy to read, well documented code
+ Transparent, easy to read, well documented workflows (e.g. data processing steps and analysis)
+ Software version control
+ Computer environment logging (e.g. what tools, what versions, what OS)
+ Parameter logging

There are many guidelines and thoughts (see below for a few suggestions).

Data analysis (of any size) should aim to have:

+ Clear, documented code
+ Ideally automation and re-usability
+ Unit testing at its basic: does my new code change my expected results?

We've started with the EpiCompBio_ GitHub account

.. _EpiCompBio: https://github.com/EpiCompBio/

There are many tools out there that aim to put the above into practice (see list of pipeline review references for example).

We don't need to re-invent the wheel, simply to make best use of our collective skills and existing tools/approaches.

See the suggested approach and tools for what we are thinking of and currently implementing/using as well as the repos and tools that are/will appear in the EpiCompBio group.


Some references and tutorials
#############################

Git and GitHub
==============

`A 15 minute intro to GitHub`_

.. _`A 15 minute intro to GitHub`: https://try.github.io/levels/1/challenges/1

`Git cheatsheet`_

.. _`Git cheatsheet`: http://ndpsoftware.com/git-cheatsheet.html

GitHub training_ and `on demand`_.

.. _`on demand`: https://github.github.io/on-demand/

.. _training: https://services.github.com/training/



Other training resources
========================

Software Carpentry's (SC) `git novice`_

.. _`git novice`: http://swcarpentry.github.io/git-novice/



Unix and command line basics
============================

`Basic tutorial`_ 

.. _`Basic tutorial`: http://www.ee.surrey.ac.uk/Teaching/Unix/index.html

`SC shell novice`_

.. _`SC shell novice`: http://swcarpentry.github.io/shell-novice/

`Code Academy command line`_

.. _`Code Academy command line`: https://www.codecademy.com/learn/learn-the-command-line


References on data analysis and reproducibility
###############################################

`PLOS Biology: Best Practices for Scientific Computing`_

.. _`PLOS Biology: Best Practices for Scientific Computing`: http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745

`PLOS Computational Biology: A Quick Guide to Organizing Computational Biology Projects`_

.. _`PLOS Computational Biology: A Quick Guide to Organizing Computational Biology Projects`: http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424

`PLOS Computational Biology: Ten Simple Rules for a Computational Biologist's Laboratory Notebook`_

.. _`PLOS Computational Biology: Ten Simple Rules for a Computational Biologist's Laboratory Notebook`: http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004385

`Reproducible Research in Computational Science`_

.. _`Reproducible Research in Computational Science`: http://science.sciencemag.org/content/334/6060/1226

`Enhancing reproducibility for computational methods`_

.. _`Enhancing reproducibility for computational methods`: http://science.sciencemag.org/content/354/6317/1240.full

`Liberating field science samples and data`_

.. _`Liberating field science samples and data`: http://science.sciencemag.org/content/351/6277/1024.full

`Promoting an open research culture`_

.. _`Promoting an open research culture`: http://science.sciencemag.org/content/348/6242/1422.full
