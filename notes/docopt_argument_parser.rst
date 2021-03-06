#####################################################
Notes on using Docopt for script command line options
#####################################################

Docopt: 

http://docopt.org/

https://github.com/docopt/docopt

An example for loading arguments from an `INI file`_:

.. _`INI file`: https://github.com/docopt/docopt/blob/master/examples/config_file_example.py

`Help message format`_

.. _`Help message format`: http://docopt.readthedocs.io/en/latest/#help-message-format

 Basic reminders for docopt:

- Use two spaces to separate options with their informal description
- () are required, [] are optional
- Default values are specified in the Options section with eg [default: xxx.log]

See also `Schema for input argument validation example`_.

.. _`Schema for input argument validation example`: https://github.com/docopt/docopt/blob/master/examples/validation_example.py

".. Usage" pattern in docopt can't have empty lines and ends with an empty line.

The first word after "Usage:" is interpreted as the program's name, e.g.:

   'python xxx.py' makes it think your programme is called 'python' with
    option 'xxx.py'

Docopt reads multi-line descriptions in Options so 80 character lines can be wrapped.

'Usage' and 'Options' case insensitive and followed by ':' are recognised by docopt in the docstrings.


R script examples and notes
###########################

Simple example (shebangs are the first line in a real script):

.. code-block::

    #!/usr/bin/Rscript

    "This is my incredible script

    Usage: my_inc_script.R [-v --output=<output>] FILE

    " -> doc

    library(docopt)
    my_opts <- docopt(doc)

That's it in order to have command line options for R scripts.

Docopt basically reads the message string and converts these to a dictionary that is then passed on.

------

*Second case*

.. code-block:: 
    
    #!/usr/bin/env Rscript

    require(docopt)
    require(methods)

    "

    Usage:
      rand-unif [--number=<number>] [--min=<min>] [--max=<max>]
      rand-unif (-h | --help | --version)

    Description:   This program generates random unifom numbers.

    Options:
          --version       Show the current version.
          --number=<num>  [default: 1] The number of random numbers to generate.
          --min=<min>     [default: 0] The lowest value a random number can have.
          --max=<max>     [default: 1] The highest value a random number can have.
    
    " -> doc

    args    <- docopt(doc)

    minimum <- as.numeric(args $ `--min`)
    maximum <- as.numeric(args $ `--max`)
    number  <- as.numeric(args $ `--number`)

    cat(paste0(runif(number, minimum, maximum), collapse = '\n'), '\n')


See how to specify the arguments and options (docopt has been ported to many languages):

- http://docopt.org/
- https://github.com/docopt/docopt.R
- https://github.com/docopt/docopt

See examples:

- http://www.slideshare.net/EdwindeJonge1/docopt-user2014
- http://rgrannell1.github.io/blog/2014/08/04/command-line-interfaces-in-r/
- https://realpython.com/blog/python/comparing-python-command-line-parsing-libraries-argparse-docopt-click/
