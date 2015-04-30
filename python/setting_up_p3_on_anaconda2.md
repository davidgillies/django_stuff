With Anaconda for python version 2.7 installed.  At the command prompt:

    conda create -n py3k python=3 anaconda
    
This sets up a virtual environment on Conda but it is different from a normal virtualenv in that it can be activated anywhere.
To use it in local P3 environments activate the environment:

    activate py3k 
    
Now install virtualenv and use in the normal way.  It will install P3 environments.

To get iPython Notebooks to work (on Windows), create a shortcut on the desktop pointing at the python 3 executable in the Anaconda environment, e.g.
C:\Anaconda\envs\py3k\python.exe 

Now right click on the shortcut and change the target to point at the relevant script with args, like this:
C:\Anaconda\envs\py3k\python.exe "C:\Anaconda\envs\py3k\Scripts/ipython-script.py" notebook

