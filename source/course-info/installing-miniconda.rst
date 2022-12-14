Install Python + libraries
==========================

The purpose of this page is to help you to install Python and different Python packages into your own computer.
Even though it is possible to install Python from the `Python homepage <https://www.python.org/>`_, **we highly recommend using** `Miniconda <https://docs.conda.io/en/latest/miniconda.html>`_ to install Python.
Miniconda comes with Python and a small number of essential packages.
Additional packages can be installed using the package management systems `mamba <https://mamba.readthedocs.io/en/latest/index.html>`_ or `conda <https://docs.conda.io/en/latest/>`__.
Both offer similar functionality, but we suggest using mamba because it is significantly faster for installing the libraries needed for using Python for GIS.

Miniconda is a light-weight version of `Anaconda <https://www.anaconda.com/>`_ which is an open source distribution of the Python and R programming
languages for large-scale data processing, predictive analytics, and scientific computing, that aims to simplify package management and deployment. In short,
it makes life much easier when installing new tools to your Python.

In case you already have Anaconda installed on your computer, you can continue using that during the course without a problem.
**If you are new to Python and have not yet installed anything, we recommend you to start by**
`installing Miniconda <https://docs.conda.io/en/latest/miniconda.html>`__.

Install Miniconda
-------------------

You can find the latest version of Miniconda for different operating systems in the `Miniconda dowload page <https://docs.conda.io/en/latest/miniconda.html>`__.
Tips and tricks for Windows, macOS and Linux users below.

Windows
~~~~~~~~

Visit the `Miniconda download page <https://docs.conda.io/en/latest/miniconda.html#windows-installers>`__ and download the latest
**Miniconda3 Windows 64-bit** installer for Windows.

.. figure:: img/miniconda-windows.png
    :width: 600px
    :align: center
    :alt: Downloading the latest Miniconda for Windows

Install Miniconda to your computer by double clicking the installer and install it into a directory you want (you might need admin rights).
Install it to **local user** and use the default settings.

After the installation is completed, test that the package manager ``conda`` works by
`opening an ``Anaconda prompt (miniconda3)`` from the start menu,
and running command ``conda --version``. If the command returns a version number of conda (e.g. ``conda 4.5.9``) everything is working correctly.

macOS
~~~~~~~~
Visit the `Miniconda download page <https://docs.conda.io/en/latest/miniconda.html#macosx-installers>`__ and download the latest
Python 3.8 installer for macOSX.

.. figure:: img/miniconda-osx.png
    :width: 600px
    :align: center
    :alt: Downloading the latest Miniconda for Mac

Linux
~~~~~

Install Miniconda 3 and add it to system path using Terminal:

.. code-block::

    # Download and install miniconda (first
    sudo wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    sudo bash Miniconda3-latest-Linux-x86_64.sh

    # Add miniconda installation permanently to PATH variable
    nano ~/.bashrc

    # Add following line at the end of the file and save (EDIT ACCORDING YOUR INSTALLATION PATH)
    export PATH=$PATH:/PATH_TO_MINICONDA/miniconda3/bin:/PATH_TO_MINICONDA/miniconda3/lib/python3.8/site-packages

Install the course environment
------------------------------

Installing various GIS packages in Python can be sometimes a bit tricky due to various dependencies
between the packages. Sometimes an older version of the package, or even an older Python version might be required for a
specific tool to work. The recommended way to get the installation working smoothly is to **create a dedicated
Python environment** for the selected Python packages (e.g. for the ones used during this course).
A python environment is a separate installation including all required libraries as well as
the Python interpreter. It is a good practice to install all packages (if possible) from the same
conda channel (e.g. ``conda-forge`` which we recommend), and not to mix conda and pip for installations
if not strictly necessary.

Conda has an excellent documentation about `creating and managing conda environments <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`__
where you can check details of the used commands.

Installing mamba
~~~~~~~~~~~~~~~~

To get started we will install the mamba package manager in our new Miniconda environment (are you tired of all the snake references yet?).
We can install mamba by **opening an Anaconda prompt (miniconda)** and running the following:

.. code-block:: bash

    # Install mamba
    conda install mamba -n base -c conda-forge

If you're curious, you can find more about mamba in the `online user guide <https://mamba.readthedocs.io/en/latest/index.html>`__ which covers most of the basic things, such as installing new packages.

Installing the packages
~~~~~~~~~~~~~~~~~~~~~~~

After installing `mamba`, the main steps for creating and using a conda environment:

1. create the environment from environment.yml file using mamba,
2. activate the environment
3. start using the environment (e.g. launch the JupyterLab and start coding, see below)

We have prepared a ready-made environment file for this course (called ``environment_mini.yml``). You can  `DOWNLOAD IT FROM HERE <https://github.com/htenkanen/mobility-course/blob/main/ci/environment_mini.yml>`__.
After downloading the environment file, run the following commands on the same folder where you downloaded it.
If you don't know how to navigate between different folders, check these short tutorials for `terminal <https://riptutorial.com/terminal/example/26023/basic-navigation-commands>`_ and `command prompt (Windows) <https://riptutorial.com/cmd/example/8646/navigating-in-cmd>`_.
The commands below work similarly in all operating systems where you have Miniconda (or Anaconda) installed:

1. Create the Python environment based on the file that you downloaded by using a terminal (or command prompt)
and executing the following command in the directory where you downloaded the `.yml` file:

.. code-block::

    mamba env create -f environment.yml


2. Activate the environment:

.. code-block::

    conda activate geo

You should now see the name of the environment at the start of the command line.

3. Launch JupyterLab IDE

After you have installed all required packages, you can start working in a local Jupyter Lab environment that is
linked to your ``geo`` conda environment by launching jupyter lab on the command line.

It's a good idea to first navigate to the folder where your Jupyter Notebook -files are located before launching Jupyter Lab.

.. code-block::

    jupyter lab

Note, Jupyter Lab will probably prompt you to "Build" the installation in order to get the git-plugin to show.

.. hint::

    If you want to install some additional packages to your conda environment, ensure you have activated it (step 2 above) and
    install the package that you wish to install following the guidelines below.

Install OpenJDK Java Development Kit
------------------------------------

``r5py`` library relies on Java JDK engine. Hence to get the ``r5py`` working, you need to install OpenJDK to your computer.
Below are instructions how to do that.

Windows
~~~~~~~~

On Windows, you need to do a bit of manual work to get OpenJDK working. Follow these steps:

1. Go to `https://jdk.java.net/java-se-ri/11 <https://jdk.java.net/java-se-ri/11>`__ website
2. Download the ``Windows/x64 Java Development Kit`` ((sha256) 178.7 MB) from the site by pressing the link
3. Extract the contents of the Zipfile to your computer, e.g. ``Downloads``. As a result, you should see a folder called ``jdk-11``.
4. Under the ``C:\Program Files`` create a folder called ``Java`` (requires admin rights)
5. Copy and paste the ``jdk-11`` folder into the newly create ``C:\Program Files\Java`` directory (requires admin rights).
6. Open a command prompt in **admin mode** by typing ``cmd`` in the Start menu -> **right click** the Command Prompt icon -> choose ``Run as administrator``.
7. Once you have the command prompt open in admin mode, type ``setx -m JAVA_HOME "C:\Program Files\Java\jdk-11\bin"`` which will create an environment variable called ``JAVA_HOME`` for your computer which points to the folder where we copied the ``jdk-11``.
8. Close the command prompt
9. Open ``Anaconda Prompt (miniconda)`` from the start menu
10. Activate the ``geo`` environment by typing ``conda activate geo``
11. Run command ``python -c "import r5py"``. If this does not produce any errors, everything works!

Linux/Mac
~~~~~~~~~

On Linux and Mac, getting the OpenJDK working is slightly easier ...

1. Activate the ``geo`` environment by typing ``conda activate geo`` in a terminal
2. Install the ``openjdk`` by typing ``mamba install -c conda-forge openjdk=>17.0.3``
3. Close the terminal. Open the terminal again.
4. Activate the ``geo`` environment by typing ``conda activate geo``
5. Run command ``python -c "import r5py"``. If this does not produce any errors, everything works!

General guide for installing packages with Mamba/Conda
------------------------------------------------------

Conda has an excellent `online user guide <https://docs.conda.io/projects/conda/en/latest/index.html>`__ which covers most of the basic things,
such as installing new packages. You can replace all `conda` commands listed in the user guide with `mamba` to be able to install the packages much faster.

Mamba install
~~~~~~~~~~~~~

You can install new packages using the `mamba install <https://docs.conda.io/projects/conda/en/latest/commands/install.html>`__
command. The basic syntax for installing packages is ``mamba install package-name``.
In addition, we also want to specify the **conda channel** from where the package is downloaded using the parameter `-c`.

**Installing Pandas package from the conda-forge channel:**

.. code-block::

    mamba install -c conda-forge pandas

Once you run this command, you will see also other packages getting installed and/or updated as conda checks for dependencies of the installed package.
Read more about package installations in the `conda documentation <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html#installing-packages>`__
It's a good idea to search for installation instructions for each package online.

You can **install other useful packages in a similar way:**

.. code-block::

    mamba install -c conda-forge matplotlib
    mamba install -c conda-forge bokeh
    mamba install -c conda-forge geopandas

.. admonition:: Conda channels

    `Conda channels <https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html>`__ are remote locations where packages are stored.
    During this course (and in general when installing packages for scientific computing and GIS analysis) we download most packages from the `conda-forge <https://conda-forge.org/#about>`__ channel.


.. admonition:: Conflicting packages

    A good rule of thumb is to **always install packages from the same channel** (for this course, we prefer the `conda-forge` channel).
    In case you encounter an error message when installing new packages, you might want to first check the versions and channels of existing
    packages using the `conda list` command before trying again.

Installing JupyterLab
~~~~~~~~~~~~~~~~~~~~~~~

We use `JupyterLab <https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html>`__ as the main programming environment during this course.
JupyterLab can be installed like any other packages using the conda install command.

For other options and more information, take a look at the `JupyterLab installation instructions <https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html>`__.

**Install JupyterLab from the conda-forge channel:**

.. code-block::

    mamba install -c conda-forge jupyterlab

After installation is completed, you can start a JupyterLab instance by running this command (notice the space between the words!):

.. code-block::

    jupyter lab

After running the command, JupyterLab should open up automatically in a browser window.

Git extension for JupyterLab
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After you have installed JupyterLab, you can also add the JupyterLab Git extension to your environment:

.. code-block::

    conda install -c conda-forge jupyterlab-git

