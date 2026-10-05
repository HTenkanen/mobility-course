Install Python + libraries
==========================

This page shows you how to install Python and the Python libraries that we use during this course on your own computer.
Even though it is possible to install Python from the `Python homepage <https://www.python.org/>`__, we recommend using
`Miniconda <https://www.anaconda.com/docs/getting-started/miniconda/install>`__ to install Python.
Miniconda is a lightweight Python distribution that comes with the Python interpreter, a small number of essential packages,
and the **conda** package manager. A **package manager** is a tool that installs Python libraries for you and resolves the
dependencies between them, i.e. it picks versions of the libraries that work together.

The installation has two steps:

1. Install Miniconda on your computer.
2. Use conda to create the course environment, which contains all the libraries that we use during the course.

In case you already have Anaconda or Miniconda installed on your computer, you can use it during the course and continue
directly to :ref:`install-course-environment`.

Install Miniconda
-----------------

Pick the installer for your operating system below. The links always point to the latest version of Miniconda.
You can find more details in the `Miniconda installation guide <https://www.anaconda.com/docs/getting-started/miniconda/install>`__.

Windows
~~~~~~~

Download the `Miniconda installer for Windows <https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe>`__
and double-click the downloaded file to start the installation. You can use the default options, but pay attention to the installation type:

- **Just Me** (recommended): Miniconda is available only for your user account. This does not require administrator rights.
- **All Users**: Miniconda is available for all users of the computer. This requires administrator rights.

After the installation has completed, test that conda works by opening **Anaconda Prompt** from the Start menu and running the following command:

.. code-block:: bash

    conda --version

If the command prints a version number of conda, everything works correctly.

macOS
~~~~~

Download the graphical installer that matches the processor of your computer:

- `Apple Silicon <https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.pkg>`__ (M1, M2, M3, M4 and later processors)
- `Intel <https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.pkg>`__

You can check which processor your computer has from the Apple menu → **About This Mac**.
Double-click the downloaded file and follow the steps of the installer; you can use the default options.
After the installation has completed, open a new **Terminal** window and run:

.. code-block:: bash

    conda --version

If the command prints a version number of conda, everything works correctly.

Linux
~~~~~

Open a terminal, then download and run the installer:

.. code-block:: bash

    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    bash Miniconda3-latest-Linux-x86_64.sh

The installer asks you to accept the license terms and, at the end, whether to update your shell profile to automatically initialize conda.
Answer ``yes`` to both. Installing Miniconda to your home directory (the default location) does not require administrator rights.
If your computer has an ARM processor, use ``Miniconda3-latest-Linux-aarch64.sh`` instead.

After the installation has completed, close the terminal, open a new one and run ``conda --version``.
If the command prints a version number of conda, everything works correctly.

.. _install-course-environment:

Install the course environment
------------------------------

Installing GIS libraries for Python can sometimes be a bit tricky, because many of them depend on each other and need
compatible versions. Therefore, we recommend installing the libraries used during this course into a dedicated
**conda environment**. A conda environment is an isolated Python installation with its own Python interpreter and libraries.
You can have several environments on your computer (e.g. one for each course or project) and switch between them with a single command.

We have listed all the libraries needed during the course in an **environment file** written in the YAML format.
With this file, you can create the whole environment with one command:

1. **Download the environment file**: :download:`environment.yml <../../ci/environment.yml>`.

2. **Create the environment.** Open Anaconda Prompt (Windows) or Terminal (macOS and Linux), change to the folder where
   you saved the file, and run the following commands:

   .. code-block:: bash

       # Change to the folder containing the environment file
       cd path/to/download/folder

       # Create the environment
       conda env create -f environment.yml

   During this step, conda downloads several hundred megabytes of packages, so it can take several minutes.
   Most of the libraries come from the `conda-forge <https://conda-forge.org/>`__ channel. A few course libraries
   (``cafein``, ``cafein.lca``, ``cafein.sampledata``, ``transitio`` and ``transitio-editor``) are available only from
   the Python Package Index (PyPI). conda installs them with ``pip`` at the end of the same command, so you don't need to do anything extra.

   If you don't know how to move between folders on the command line, check these short tutorials for the
   `terminal <https://riptutorial.com/terminal/example/26023/basic-navigation-commands>`__ (macOS and Linux) and the
   `command prompt <https://riptutorial.com/cmd/example/8646/navigating-in-cmd>`__ (Windows).

3. **Activate the environment**:

   .. code-block:: bash

       conda activate sumogis

   You should now see ``(sumogis)`` at the start of the command line. Activate the environment every time you open
   a new terminal window to work with the course materials.

4. **Test the installation** by running the following command:

   .. code-block:: bash

       python -c "import geopandas, pyrosm, cafein, transitio"

   If the command finishes without errors, everything works! The command can take a while the first time you run it.
   If you get an error, check that you have activated the environment (step 3) and that step 2 finished without errors.

5. **Launch JupyterLab**, which we use as the main programming environment during the course:

   .. code-block:: bash

       jupyter lab

   JupyterLab opens in a browser window, in the folder from which you launched it. Therefore, it is a good idea to first
   change to the folder where your notebooks are located before launching JupyterLab.

Installing additional libraries
-------------------------------

You can install new packages to the active environment using the ``conda install`` command.
The basic syntax for installing packages is ``conda install package-name``. In addition, we recommend specifying the
**conda channel** from where the package is downloaded using the parameter ``-c``. For instance, you can install the
``seaborn`` library from the conda-forge channel as follows:

.. code-block:: bash

    conda install -c conda-forge seaborn

Once you run this command, you will also see other packages getting installed and/or updated as conda checks the
dependencies of the new package. It's a good idea to search for the installation instructions of each package online.
You can read more about `managing environments <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html>`__
and `installing packages <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-pkgs.html>`__ in the conda documentation.

.. admonition:: Conda channels

    `Conda channels <https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html>`__ are remote locations where packages are stored.
    During this course (and in general when installing packages for scientific computing and GIS analysis) we download most packages from the `conda-forge <https://conda-forge.org/>`__ channel.

.. admonition:: Conflicting packages

    A good rule of thumb is to **always install packages from the same channel** (for this course, we prefer the conda-forge channel).
    In case you encounter an error message when installing new packages, you might want to first check the versions and channels of existing
    packages using the ``conda list`` command before trying again.
