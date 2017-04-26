#######################################################
Notes on computational pipelines for biomedial research
#######################################################

:Author: Antonio Berlanga
:Date: 22 Dec 2016

(Disclaimer (!): I've been learning as I go and I still have a long way... Please add, discuss, correct, etc.)


Suggested tools and approach to implement in computational and statistical analysis
###################################################################################

Conceptually the problem is simple: chain third party tools and custom scripts together to answer a specific scientific question.

In practice this is a nightmare. It requires project discipline and very good statistical and scripting practices.

For example, in a genetic association project you might need: 

+ Genotype QC pipeline
+ Imputation pipeline
+ Association testing pipeline
+ Downstream annotation of significant SNPs

All of these require many programs (third party like plink), some custom scripts (like plotting and stats in R) and will probably need to be run in a high performance cluster.

Keeping track of results, re-running with different parameters, logging, version control, communicating with colleagues, etc. quickly becomes difficult. A systematic approach is needed from the beginning that will cut the overhead and allow all results and plots to be traced back to the commands, parameters, software versions, and any steps used to process the original data, in an easy, transparent and reproducible way.

I have failed to do this and over time the costs can be high.

There are many tools out there that aim to put reproducibility in computational biology (or general data analysis) into practice (see list of pipeline review references for example).

Reproducibility requires data + code

We don't need to re-invent the wheel, simply to make best use of our collective skills and existing tools/approaches.

Sound principles come first, languages and tools are secondary (to an extent, tools over time shape our thinking so good initial choices are important).

However a general, common framework and way of working is necessary. After a lot of initial personal and group pain we should hopefully see gains.


Using Python and UNIX philosophy as the building bases
######################################################

Python_:

	Python is a popular, well-supported, general programming language which is flexible, powerful and readable. A great choice overall for beginners. It can serve as the glue for pipelines even if many scripts and programs are in other languages. Ruby, Perl and others are largely equivalent. There are dozens of online source for learning and a very active community.

.. _Python: https://www.python.org/

Ultimately a combination of unix (or equivalent compute environment), stats and programming is needed. Different people do/use different combinations.

Using python, R and Unix is pretty powerful and a well trodden path.

The main/basic idea is to be able to structure scripts into packages and re-use them (or at least freeze and present them at publication).

There's a lot out there on software structure, see for example:

	`Design patterns : elements of reusable object-oriented software`_
	
.. _`Design patterns : elements of reusable object-oriented software`: https://www.amazon.co.uk/gp/product/0201633612/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0201633612&linkCode=as2&tag=anjabl-20
	
	`Python Project Howto`_
	
.. _`Python Project Howto`: http://infinitemonkeycorps.net/docs/pph/

	`Organising my Python project`_ - Stack Overflow
	
.. _`Organising my Python project`: http://stackoverflow.com/questions/391879/organising-my-python-project

	`Filesystem structure of a Python project`_ - Jp Calderone
	
.. _`Filesystem structure of a Python project`: http://jcalderone.livejournal.com/39794.html

	`Structuring Your Project`_ — The Hitchhiker's Guide to Python
	
.. _`Structuring Your Project`: http://docs.python-guide.org/en/latest/writing/structure/


	`Software Carpentry`_ - Intermediate and Advanced

.. _`Software Carpentry`: http://intermediate-and-advanced-software-carpentry.readthedocs.io/en/latest/structuring-python.html


UNIX is at the heart of most of the common and powerful operating systems available. See: 

Phylosophy_
	
.. _Phylosophy: https://en.wikipedia.org/wiki/Unix_philosophy
	
`A classic book on UNIX`_:

	The Unix Programming Environment (Prentice-Hall Software Series) Paperback – 1 Nov 1983 by Brian W. Kernighan (Author), Rob Pike (Author)
		
.. _`A classic book on UNIX`: http://cs2.ist.unomaha.edu/~stanw/163/csci4500/UNIXProgrammingEnvironment.pdf

`A general update on the above`_: 

	The Art of Unix Programming (Addison-Wesley Professional Computing) Paperback – 23 Sep 2003 by Eric S. Raymond (Author)
		
.. _`A general update on the above`: https://www.amazon.co.uk/Unix-Programming-Addison-Wesley-Professional-Computing/dp/0131429019


Actual tools and practice
#########################

In general, pipelines should ideally be:

+ Well documented
+ Configurable for available compute resources
+ Not hard-coded: configurable for actual job parameters which will be arbitrary and project specific probably
+ Run from the command line 
+ Report extensive logging for debugging and versioning
+ Easy to build on
+ Runnable locally or on a cluster
+ Able to handle single and multi-jobs
+ Portable across computational environments
+ ...

A big problem across the field is portability, currently without good answers, but pipelines can go some way towards this.
	
The general approach I'm suggesting is the one used at CGAT_, which in turn adopts many current computational best practice standards). See:

.. _CGAT: www.cgat.org

+ https://github.com/CGATOxford
+ https://github.com/CGATOxford/cgat
+ https://github.com/CGATOxford/CGATPipelines
+ https://www.software.ac.uk/tags/cgat
+ https://www.software.ac.uk/blog/2016-09-27-introduction-cgat

The CGAT Code Collection includes cgat scripts for genomics and CGAT Pipelines, a framework and set of ruffus based pipelines to run workflows in computational biology.

CGAT scripts and pipelines use popular, open source, mostly free, proven tools with excellent community support such as Python, R, Github, Travis CI, plus the myriad of genomics and biology software options for specific tasks.

A lot of this work is in beta (as are most pipeline approaches, of which there are many, galaxy is a well known one and could be an answer but version control, scalability and other issues exist, it is designed to ease use for biologists and works well like this). See Galaxy_ and the Biostars_ community for example.

.. _Galaxy: https://en.wikipedia.org/wiki/Galaxy_(computational_biology)
.. _Biostars: https://www.biostars.org/p/50034/

CGAT is based on Ruffus_, a python pipeline tool which is flexible, powerful and readable (being python).

.. _Ruffus: http://www.ruffus.org.uk/

CGAT Pipelines can help manage computer resources, clusters, logging, execution, versioning and, more importantly, to work under a common framework (think languages, style, choice of tools, etc.).

CGAT Pipelines have their own backbone (for controlling jobs, communicating with the cluster, logging, software/package structuring, etc.). I'm still on the learning curve but think this is one of the best approaches because of its flexibility and power (once you get to grips with it). `See the backbone scripts`_.

.. _`See the backbone scripts`: https://github.com/CGATOxford/CGATPipelines/tree/master/CGATPipelines/Pipeline


A pipeline example can be:

+ https://www.cgat.org/downloads/public/cgatpipelines/documentation/pipelines/pipeline_mapping.html
+ https://github.com/CGATOxford/CGATPipelines/tree/master/CGATPipelines/pipeline_mapping
+ https://github.com/CGATOxford/CGATPipelines/blob/master/CGATPipelines/PipelineMapping.py
+ https://github.com/CGATOxford/CGATPipelines/blob/master/CGATPipelines/pipeline_mapping.py


Limitations of CGAT (but common to these types of tools) are:

+ Pipelines have many dependencies
+ Setting up the initial environment is often very problematic
+ Keeping track of packages and managing them is a big overhead
+ There's a steep learning curve in general and to each pipeline/approach
+ The "system" (eg funders and current science practice) rewards results not repeatability, so no time and little interest

An excellent complement/alternative is Jupyter and its notebook (aka IPython), particularly for interactive work:

+ http://jupyter.org/
+ http://nbviewer.jupyter.org/
+ The notebook needs windowing, not great when working remotely. It can be set up though and JupyterHub server can (?) solve using notebooks to interact with a cluster (e.g. submitting notebooks as jobs).
+ Notebooks can be run locally but submitting jobs remotely:

	- https://zonca.github.io/2015/04/jupyterhub-hpc.html
	- http://ipyrad.readthedocs.io/HPC_Tunnel.html
	
On a side note, for managing packages see Conda_, a great way to reduce time spent on this.

.. _Conda: http://conda.pydata.org/docs/index.html


Structuring code
################

A general, proven approach to follow is one based on basic python organisation:

+ Scripts - Write stand-alone scripts which are callable from the CLI and can take arbitrary parameters
+ Modules - Include functions and code which could be used by more than one script/pipeline, bundled by overall aim/use
+ Pipeline - a (e.g. ruffus) python script which chains multiple tasks (e.g. functions or steps needed to obtain an answer to the project's question) and jobs (input data, e.g. you have 10 fastq files which will all be treated in the same way) and can be submitted to the cluster (e.g. managed by drmaa which will then communicate with SGE or PBSPro).

To this, we can ideally add:

+ Unit tests - aiming to test each script, parameter, function, with small, example data. Aimed for stability only (ie do new code changes mess up the expected results?). 
+ A good option is to use via Travis CI or Jenkins CI, integrated to GitHub (tests are automatically triggered after each commit, need configuration (eg yaml), data and expected result).
+ Report - aiming to write a basic automated report that picks up some basic stats, tables and plots from the pipeline results and puts them in one document (using e.g. sphinx, markdown, or similar tool).



Tools to use
############

All of the above can be achieved with:

+ Version control such as Github
+ Unit testing such as Travis (runs with Github)
+ Choice of programming and statistical languages (e.g. Python, Perl, R, Matlab, etc)
+ Computation pipeline tool such as Ruffus
+ Sufficient computing resources: your laptop, a unix cluster, etc. depending on tasks and data
+ A general framework which is extendable, allows us to keep relatively sane, and enhances the above (CGAT Pipelines, Galaxy, etc.).


Other languages
###############

In terms of packaging and structuring of projects and programs other languages do their own thing.

For examples of R_ and its repository_ take a look at:

+ `R package primer`_
+ See this package `for an R example`_.
+ `Welcome: R packages`_
+ `Developing Packages with RStudio`_ – RStudio Support
+ `Package Development Prerequisites`_ – RStudio Support
+ `E.W.Dijkstra Archive: The Humble Programmer`_
+ `Working with R on a Cluster`_ - The Coatless Professor

.. _R: https://cran.r-project.org/index.html
.. _repository: https://cran.r-project.org/web/packages/policies.html
.. _`R package primer`:	http://r-pkgs.had.co.nz/
.. _`for an R example`: http://kbroman.org/pkg_primer/
.. _`Welcome: R packages`: https://support.rstudio.com/hc/en-us/articles/200486488-Developing-Packages-with-RStudio
.. _`Developing Packages with RStudio`: https://support.rstudio.com/hc/en-us/articles/200486498-Package-Development-Prerequisites
.. _`Package Development Prerequisites`: http://www.cs.utexas.edu/~EWD/transcriptions/EWD03xx/EWD340.html
.. _`E.W.Dijkstra Archive The Humble Programmer`: http://thecoatlessprofessor.com/programming/working-with-r-on-a-cluster/
.. _`Working with R on a Cluster`: http://thecoatlessprofessor.com/programming/working-with-r-on-a-cluster/
