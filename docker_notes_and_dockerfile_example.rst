############################################
Docker workflow notes and Dockerfile example
############################################

:Author: Antonio J Berlanga-Taylor
:Date: July 3 2016


Docker_ is software for container platforms. Containers are like virtual machines (but generally better, see links below).

You can use Docker to develop tools in your local machine (regardless of its own operating system) and test without worrying about how your software will perform in a different environment.

Docker automates setting up and configuring environments. This makes it easy to build software, collaborate with others in data analysis, etc.

You can specify in your Dockerfile all the needed dependencies and instructions to run your application, scripts, etc.

Your application could be software for others or even your specific data analysis project.

The Dockerfile can be like a lab notebook containing instructions on the computing environment, external and internal software, versions used and example data for instance.

Learning Docker and writing a Dockerfile may be time consuming initially but could save you and collaborators  major headaches when you try to reproduce results.

You can find many and better tutorials online and in the official `Docker documentation`_. As with other files in this repository, these are basic notes, links and reminders to get started.

.. _Docker: https://www.docker.com/

.. _`Docker documentation`: https://docs.docker.com/engine/getstarted/


.. note::

    Some code snipets, info, etc. is directly from some of the references. Files need cleaning up.


Docker notes
############

General steps to create a Dockerfile (see more details below):

See `Dockerfile writing best practice guidelines`_.

.. _`Dockerfile writing best practice guidelines`: https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices 

1) Create a file called Dockerfile, which we will use to place the relevant instructions and commands that will define what our container can do
2) Build the Docker container, this will install and apply all the environment variables and configurations that you have specified in the Dockerfile
3) Run the Dockerfile across any computing platform (with Docker installed on that platform).

Alternatively, use a pre-specified image with all the tools you need. Anything that isn't in the Dockerfile though is not kept (ie any new tools which are installed).

Base image with all the tools needed except the application itself:

	- Linux distro
	- Python
	- R
	- Conda
 	- Apline Linux (minimalistic)

Copy the Dockerfile, e.g.:

- https://hub.docker.com/r/continuumio/miniconda3/~/dockerfile/

Add necessary tools to it and run as in steps above.

Otherwise, pull already available image and work from there:

Do e.g.:

.. code-block:: bash 
	
	docker pull continuumio/miniconda3
	docker run -i -t continuumio/miniconda3 /bin/bash


Data science base images:

- https://hub.docker.com/r/continuumio/miniconda3/
- https://hub.docker.com/r/continuumio/anaconda3/
- https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science

`Alpine Linux`_ (5 MB) is a minimal image that can serve as a starting point.

.. _`Alpine Linux`: https://hub.docker.com/r/library/alpine/

With this use Dockerfile containing e.g.:

.. code-block:: bash

	FROM alpine:3.3
	RUN apk add --no-cache mysql-client
	ENTRYPOINT ["mysql"]


Steps to create a Dockerfile
############################

1) Write a dockerfile, see:

- https://docs.docker.com/engine/getstarted/step_four/
- https://docs.docker.com/engine/getstarted/step_four/#step-4-run-your-new-docker-whale

Dockerfile for data science examples:

- http://tlfvincent.github.io/2016/04/30/data-science-with-docker/
- https://www.dataquest.io/blog/docker-data-science/

`Minimal alpine Python 3 image`_ example.

.. _`Minimal alpine Python 3 image`: https://github.com/jfloff/alpine-python

-----

Dockerfile contents:

.. code-block:: bash

	# specifiy base image
	FROM ubuntu:14.04 # also FROM jupyter/scipy-notebook

	# provide creator/maintainer of this Dockerfile
	MAINTAINER Antonio J Berlanga-Taylor <a.berlanga@imperial.ac.uk>

	# Specify some of the useful system tools and libraries to include in the Ubuntu bare bones image:

	# Update the sources list
	RUN apt-get update
	# RUN cmds are linux cmds

	# install useful system tools and libraries
	RUN apt-get install -y libfreetype6-dev && \
		apt-get install -y libglib2.0-0 \
		libxext6 \
		libsm6 \
		libxrender1 \
		libblas-dev \
		liblapack-dev \
		gfortran \
		libfontconfig1 --fix-missing

	RUN apt-get install tar \
		git \
		curl \
		nano \
		wget \
		dialog \
		net-tools \
		build-essential

	# install Python and pip package manager
	# TO DO: change for conda, eg:
	# https://hub.docker.com/r/continuumio/miniconda/
	# from where jupyter can run
	RUN apt-get install -y python \
		python-dev \
		python-distribute \
		python-pip

	# install useful and/or required Python libraries to run your script
	# # TO DO: change for conda recipe, Bioc image, etc.
	RUN pip install matplotlib \
                seaborn \
                pandas \
                numpy \
                scipy \
                sklearn \
                python-dateutil \
                gensim

	COPY localfile.R /home/ubuntu/localfilecopy.R
	# COPY copies local files into the container

	EXPOSE 5000
	# opens ports that can be mapped to server ports (?)

	# define command to when Docker container starts
	ENTRYPOINT ["python"]
	CMD ["my_script.py"]
	# This is the first command that will run once the container starts
	# Note Docker doesn't accept single quotes, only double.

-----

2) Build the docker image

From within the docker terminal and from the directory where the dockerfile (and eg python script) are:

.. code-block:: bash
	
	docker build -t your_image_name .


See the messages printed and if it builds successfully it will appear in:

.. code-block:: bash

	docker image list

-----

3) Run the docker image:

Create and enter a folder where data is located and/or will be saved:

.. code-block:: bash

    cd ~/Documents/github.dir/docker_tests.dir

Install Docker on the platform to use beforehand:

https://docs.docker.com/engine/installation/linux/rhel/

.. code-block:: bash

	docker run --rm -ti your_image_name

An -it flag makes the container run interactively

\--rm automatically remove the container when exiting

Get the data (mount a volume) and point docker to it:

.. code-block:: bash

	docker run -it -d -p 8888:8888 -v /home/ubuntu/xxx:/Users/USER/data/datfile.data your_image_name


\-p flag sets the ports (to access a Jupyter notebook server locally). To find Docker's ip address use:

docker-machine ip default #'default' for docker machine

\-d runs the container in detached mode, as a background process.

\-v specifies which directory on the local machine to store results


Data/files can be copied across with docker cp

These will be lost when the container is stopped (but not results save locally) unless pre-specified in the Dockerfile.

Shut down the docker container:

.. code-block:: bash

	docker ps # to get CONTAINER_ID
	docker rm -f CONTAINER_ID


Get system info:

.. code-block:: bash
	
	docker info


`Remove old containers and images`_:

.. _`Remove old containers and images`: http://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers

.. code-block:: bash

	docker ps -a
	docker rm CONTAINER_ID
	docker images
	docker rmi IMAGE


Stop and remove all containers:

.. code-block:: bash

	docker stop $(docker ps -a -q)
	docker rm $(docker ps -a -q)


-----

Create a `Docker Hub account`_ to upload your images and make them available to others.

.. _`Docker Hub account`: https://docs.docker.com/engine/getstarted/step_five/


Testing workflow example
########################

Create a Dockerfile as above, see for example:

https://github.com/AntonioJBT/project_quickstart/blob/master/Dockerfile

See these minimal images with `Alpine and Python`_ for instance.

.. _`Alpine and Python`: https://github.com/jfloff/alpine-python

Copy Dockerfile to test directory (not necessary though), build image locally and run:

.. code-block:: bash
	
	mkdir docker_tests
	cd docker_tests
	cp ../github_xxx/project_xxx/Dockerfile . 
	docker build -t user_xxx/my_docker_tag .
	docker images
	docker run --rm -ti user_xxx/my_docker_tag

Clean up:

.. code-block:: bash

	docker images
	docker images -f "dangling=true"
	docker rmi $(docker images -f "dangling=true" -q)
	docker ps -a
	docker rm $(docker ps -a -q)


You can then go back to your code, make changes, push/pull to your version control system and start again with Dockerfile to test your package in a different environment to your machine.


TO DO
#####

- Integrate with GitHub and Travis ?
- Use dockerHub to push and pull akin to GitHub (integrate?)


Additional links and references
###############################

- https://www.nersc.gov/assets/Uploads/cug2015udi.pdf
- https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science
- http://cdn.oreillystatic.com/en/assets/1/event/144/Docker%20for%20data%20scientists%20Presentation.pdf
