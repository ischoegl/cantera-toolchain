# Windows 10 / Anaconda / Visual Studio

The installation instructions are slightly modified from 
[Bryan Weber's recommendations](https://groups.google.com/forum/?utm_medium=email&utm_source=footer#!msg/cantera-users/L4c0QJIFd0o/0ZUPLlq8BQAJ) 
on the Cantera forum.

## Anaconda

Install [Anaconda](https://www.anaconda.com/distribution/) and run an update using

```
(base) > conda update --all
```

_... using Anaconda's Python 3.7 version_

## Visual Studio

Install [Visual Studio](https://visualstudio.microsoft.com/) IDE

_... tested for Community 2019 edition_ (Desktop development with C++)

## Create a conda environment

Locate the __x64 Native Tools Command Prompt__ in the Menu, right-click, select __More > Open File Location__, right-click on 
the shortcut and copy the __Target__ command. Depending on installation it may or may not look similar to 

```
%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat"
```

Open an __Anaconda Prompt__, and create the compilation environment

```
(base) > CALL %comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat"
```

which sets all environment variables for compilation. Then, create a new conda environment using

```
(base) > conda create -n cantera-dev scons numpy cython ruamel_yaml libboost git
```

Finally, activate the new environment using

```
(base) > conda activate cantera-dev
```

## Compile Cantera

Change to a suitable installation folder, and clone the repository (or a fork thereof), e.g.

```
(cantera-dev) > git clone https://github.com/Cantera/cantera.git
(cantera-dev) > cd cantera
```

Create a cantera configuration file __cantera.conf__ with the following content (make sure to replace `<user name>` with the appropriate folder name, and adjust other path information as needed):

```
prefix = 'C:/Users/<user name>/cantera'
boost_inc_dir = 'C:/Users/<user name>/AppData/Local/Continuum/anaconda3/envs/cantera-dev/Library/include'
```

and run 

```
(cantera-dev) > scons build
(cantera-dev) > scons test
(cantera-dev) > scons install
```

The installation ends with

```
Cantera has been successfully installed.

File locations:

  applications                C:/Users/<user>/cantera\bin
  library files               C:/Users/<user>/cantera\lib
  C++ headers                 C:/Users/<user>/cantera\include
  samples                     C:/Users/<user>/cantera\samples
  data files                  C:/Users/<user>/cantera\data
  Python package (cantera)    C:\Users\<user>\AppData\Local\Continuum\anaconda3\envs\cantera-dev\Lib\site-packages
  Python samples              C:\Users\<user>\AppData\Local\Continuum\anaconda3\envs\cantera-dev\Lib\site-package\cantera\examples
scons: done building targets.
```
