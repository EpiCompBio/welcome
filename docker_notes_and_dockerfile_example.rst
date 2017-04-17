############################################
Docker workflow notes and Dockerfile example
############################################

:Author: Antonio J Berlanga-Taylor
:Date: July 3 2016


Some links and references
#########################

- https://docs.docker.com/engine/getstarted/
- https://www.nersc.gov/assets/Uploads/cug2015udi.pdf
- https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science
- http://cdn.oreillystatic.com/en/assets/1/event/144/Docker%20for%20data%20scientists%20Presentation.pdf
- https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices


TO DO
#####

- Integrate with GitHub and Travis ?
- Use dockerHub to push and pull akin to GitHub (integrate?)


Docker notes
############

General steps:

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

Copy the Dockerfile, eg:

- https://hub.docker.com/r/continuumio/miniconda3/~/dockerfile/
- Add necessary tools to it and run as in steps above.

Otherwise, pull already available image and work from there:

Do e.g.:

.. code-block:: bash 
	
	docker pull continuumio/miniconda3
	docker run -i -t continuumio/miniconda3 /bin/bash

Data science base images:

- https://hub.docker.com/r/continuumio/miniconda3/
- https://hub.docker.com/r/continuumio/anaconda3/
- https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science

Alpine Linux (5 MB) is a minimal image that can serve as a starting point:
- https://hub.docker.com/r/library/alpine/

With this use Dockerfile containing e.g.:

.. code-block:: bash

	FROM alpine:3.3
	RUN apk add --no-cache mysql-client
	ENTRYPOINT ["mysql"]


General steps to create a Dockerfile
####################################

1) Write a dockerfile 

- https://docs.docker.com/engine/getstarted/step_four/
- https://docs.docker.com/engine/getstarted/step_four/#step-4-run-your-new-docker-whale
- Dockerfile for data science example:
- http://tlfvincent.github.io/2016/04/30/data-science-with-docker/
- https://www.dataquest.io/blog/docker-data-science/

Minimal alpine Python 3 image:

- https://github.com/jfloff/alpine-python

-----

Dockerfile contents:

..code-block:: bash

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


Remove old containers and images:

http://stackoverflow.com/questions/17236796/how-to-remove-old-docker-containers

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

Create a Docker Hub account to upload your images, see:

https://docs.docker.com/engine/getstarted/step_five/


Testing workflow example
########################

Create a Dockerfile as above, see for example:

https://github.com/AntonioJBT/project_quickstart/blob/master/Dockerfile

Copy Dockerfile to test directory (not necessary though), build image locally and run:

.. code-block:: bash
	
	cp ../AntonioJBT/project_quickstart/Dockerfile . 
	docker build -t antoniojbt/project_quickstart .
	docker images
	docker run --rm -ti antoniojbt/project_quickstart

Clean up:

.. code-block:: bash

	docker images
	docker images -f "dangling=true"
	docker rmi $(docker images -f "dangling=true" -q)
	docker ps -a
	docker rm $(docker ps -a -q)
