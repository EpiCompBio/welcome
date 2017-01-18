###############################
Notes on continuous integration
###############################


.. author:: Antonio

.. date:: 18 January 2017


Did the code I just pushed change all my results? Did I introduce a bug?
########################################################################

Basic steps with Travis for Python:
  - Integrate and set GitHub and Travis to on (commits will trigger the tests)
  - Create a .travis.yml file at the root directory of the repository
  - Create a requirements.txt file at the root directory of the repository
  - Create tests to run, e.g.:
  
    https://github.com/EpiCompBio/genotype_tools/blob/master/tests/test_style.py
  
    These can go in a separate tests folder within the repo.
  
  - TO DO/Check: Consider if you need an external_dependencies.txt file, see for example:

    https://github.com/EpiCompBio/genotype_tools/blob/master/external_dependencies.txt
    
    Create to keep track?
    
  - Create a run_travis_tests.sh file at the root directory which will indicate which tests to actually run in Travis
  - Go to the Travis builds webpage, see the job log, config info, etc.
  - You can go to Travis settings and add the "build passing" logo to the README file in the repo:
    + https://matthewmoisen.com/blog/how-to-set-up-travis-ci-with-github-for-a-python-project/
    
  - Add unit tests if possible, e.g.:
    
    https://github.com/CGATOxford/cgat/blob/master/tests/bam2bam.py/tests.yaml
    

For a general example of a simple Travis setup see:

https://github.com/EpiCompBio/genotype_tools


General references
##################

Basic steps with Travis:
https://matthewmoisen.com/blog/how-to-set-up-travis-ci-with-github-for-a-python-project/

Test automation:
https://en.wikipedia.org/wiki/Test_automation

CI practices on wiki:
https://en.wikipedia.org/wiki/Continuous_integration#Best_practices

Travis CI
https://docs.travis-ci.com/user/getting-started

For Python:
https://docs.travis-ci.com/user/languages/python/

For R:
https://docs.travis-ci.com/user/languages/r/

Jenkins CI
https://jenkins.io/

Travis vs Jenkins:
http://stackoverflow.com/questions/32422264/jenkins-vs-travis-ci-which-one-would-you-use-for-a-open-source-project

