###############################
Notes on continuous integration
###############################


.. author:: Antonio

.. date:: 18 January 2017


Did the code I just pushed change all my results?
##################################################

Basic steps with Travis for Python:
  - Create a .travis.yml file at the root directory
  - Create a requirements.txt file
  - Create tests to run, e.g.:
  
    https://github.com/EpiCompBio/genotype_tools/blob/master/tests/test_style.py
  - Create a run_travis_tests.sh file at the root directory


For a general example see:

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

