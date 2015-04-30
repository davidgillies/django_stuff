With Anaconda for python version 2.7 installed.  At the command prompt:

    conda create -n py3k python=3 anaconda
    
This sets up a virtual environment on Conda but it is different from a normal virtualenv in that it can be activated anywhere.
To use it in local P3 environments activate the environment:

    activate py3k 
    
Now install virtualenv and use in the normal way.  It will install P3 environments.
