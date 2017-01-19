############
TO DO!
############

:Author: Antonio 
:Date: 22 Dec 2016


DONE:
#####
- The HPC team has installed ruffus and drmaa, these are working fine. David and I have been testing these and everything seems in order. 
- I've installed (in my user space) the CGAT scripts and pipeline framework, others may need to do this as well later on. The CGAT tools work well for me, they required some manual installation of several of the python libraries though. I also made some changes so that they could communicate with PBS Pro, these work without problems. There has been a recent switch to python 3 though so I have to test the modifications in the CGAT scripts. Not expecting problems though (famous last words)...

TO DO:
######

.. todo::
::

- Antonio, David, Vangelis, Gao: Finish building the Genotype QC tool
- Genotype QC is currently the first pipeline we'll build with these tools/approaches. Although not straightforward it'll essentially simply follow CGAT and Ruffus' workflow and tools. 
- Discuss with Ibrahim, Rui, Deborah: Matlab isn't open source, big problem: 
	+ Discuss Matlab users' needs and how principles can be applied without forcing others to learn new languages. 
	+ Can we simply creae Matlab scripts and run in Ruffus pipelines? Permissions?
	+ Matlab can still be open source (i.e. we can publish code but people without Matlab licence can't re-run/use/modify it?)

.. todo::
::

- Add (hand) visualising diagram as first step
- Integrate github with zenodo in order to deposit data, code, manuscript, etc. with DOI generation and release freeze for software citation?
	+ https://zenodo.org/
	+ https://guides.github.com/activities/citable-code/

.. todo::
::

- Integrate unit tests
- Integrate reST with e.g. Mendeley for reporting and citation manager, check bibtex
- JISCMAIL, add everyone to email list
- Code review flow/guide?
- Check /ifs/projects/proj032/src/pipeline_miRNA.py for more examples
- Also see Tom and Ian's UMI-tools: https://github.com/CGATOxford/UMI-tools 

	and paper: http://genome.cshlp.org/content/early/2017/01/18/gr.209601.116.abstract
	
	and Zenodo DOI: https://zenodo.org/record/215974
	
	Nice!
