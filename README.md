# Jupyter-Docker

The jupyter-docker python script is a convenience wrapper around the docker
commands needed to manage a
[All Spark Notebook](https://github.com/jupyter/docker-stacks/tree/master/all-spark-notebook)
docker container for running a local Jupyter notebooks.

## Installation

Prior to using the command, you must have Docker installed on your system and 
be running the docker daemon. This can be achieved easily by installing the
docker application for your specific platform:

 * [Docker for Mac](http://www.docker.com/products/docker#/mac)
 * [Docker for Windows](http://www.docker.com/products/docker#/windows)
 * [Docker for Linux](http://www.docker.com/products/docker#/linux)

After downloading and installing Docker for your platform, make sure that you
run it to start the docker daemon needed by the jupyter-docker script.

## Basic Usage

A command can be invoked with python:

    $ python jupyter-docker [COMMAND]
    
or by itself:

    $ jupyter-docker [COMMAND]
    
if you add executable permissions to the jupyter-docker script file and are
using a bash (or compatible) shell environment.

*Windows Usage Note:* On windows, the python command is not usually made 
available. Instead you will need to specify an absolute path to the python exe
such as:

    $ C:\Python3.5\python.exe jupyter-docker [COMMAND]
    
where the path to your python.exe depends on your system.

## First Use

Before you can run the jupyter container, the source files (i.e. docker image) 
need to be installed on your system. To do that execute the 'update' command:

    $ python jupyter-docker update
    
This single command will take care of the installation process for you. 
However, the files are large (5GB) and it will take some time to download.

When you execute the update command after the docker image (source files) are
already installed, the docker image (source files) will be updated if any 
updates are available. It is recommended that you run this periodically to 
make sure you are running the latest versions of all the software.

## Available Commands

The script has four available commands:

  * __start:__ starts a running container with any specified arguments. Any 
        existing container will be shut down and replaced by a new one.
  * __stop:__ stops the currently running container if one exists
  * __update:__ installs or updates the docker image on which the container is 
        run. This step will run implicitly if a' start command is issued before 
        the image has been installed.
  * __open:__ opens a bash terminal in the currently running container. This 
        gives you command line access for running python or pyspark scripts 
        outside of a notebook environment

## Notebooks

Once you have installed the docker image using the *update* command, you can
start the container running with:

    $ python jupyter-docker start
    
A container running jupyter will be started. Your home directory is also 
attached to the container with the folder name 'root'. This gives notebooks 
access to the files in your home directory. 

For notebooks run using an Anaconda Python 3 environment:

    http://localhost:8888
    
For notebooks run using Anaconda Python 2 environment:

    http://localhost:8889

When finished working, you shut the container down with the command:

    $ python jupyter-docker stop
    
# Advanced Usage

## Terminal Access

If you would like command line access to the running container, use the command:

    $ python jupyter-docker open
    
A bash shell will be opened in the container. You can use this to conda install
additional packages, run scripts from the command line or otherwise modify the
container environment where the notebooks are running.

*Note:* Any changes you make to the container will be lost when you stop the 
container.

## Additional Command Flags

The *start* command accepts flags to change the default behavior of the 
container.

   * __--directory__ Use this flag to specify an alternate directory to mount
        to the container instead of your home directory.
   * __--port__ Specifies the localhost port (default 8888) for the jupyter
        notebook server running in an Anaconda 3 environment.
   * __--port2__ Specifies the localhost port (default 8889) for the jupyter
        notebook server running in an Anaconda 2 environment.
   
