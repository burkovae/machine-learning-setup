# Setting up a project for machine learning

This repository documents my personal approach and experiments to set up a python or more specific a machine learning project.

## First things first

We want to make the fizzling with development as easy as possible - it will allow us to focus more on content instead of figuring out how to do stuff the right way.

* [`z` is super useful](https://github.com/rupa/z) - it allows you to change to directories based on patterns. You'll love it when you start to use it.
* [`pyenv` is awesome](https://github.com/pyenv/pyenv). A great to tool to [Do One Thing and Do It Well](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well): setup different python versions. (e.g. for ML with MKL we need 3.6.9, but for others 3.7.4. And maybe somebody want to try out `pypy`) - this tool is THE tool for python management.
* [`pyenv-virtualenv` for virtual environements plugin for `pyenv`](https://github.com/pyenv/pyenv-virtualenv). For every encapsulated python project. (TODO: try out using CI)

## Setting up a project (for Maschine Learning)

We want to use a performant setup and for academic usage [Intel's MKL libraries](https://software.intel.com/en-us/mkl) will give up to 10x speed increase in everything related to vector and matrices. However, as for now (2019.08) they are available for python version upto 3.6.*.

* Install python 3.6.9 with pyenv, create virtualenv `ml` based on this version.

```
pyenv install 3.6.9
pyenv virtualenv 3.6.9 ml
cd <your_project_base_dir>
pyenv local ml
```

The last command automagically activates virtual environment `ml` when we change into `<your_project_base_dir>`. No more:  `activate <where_was_my_venv_again?>`

![](images/z-ml.gif)

Additionally, install `pipenv` via `pip install pipenv` into your virtual environment.

Now for the meat: essential machine learning libraries. 
* For Windows MKL builds [look here](https://www.lfd.uci.edu/~gohlke/pythonlibs/). 
* For `tensorflow` builds that are optimal for your windows architecture (e.g. `AVX2`) [look here](https://github.com/fo40225/tensorflow-windows-wheel)
* For linux you can use either `pip install -r ml-modules` or if you want to have better dependency management (TODO: CI)

```
pipenv install -r ml-modules
```

`ml-modules.txt` contains `intel-*` (* in `numpy, scipy, scikit-learn`) - [see here Intel's python modules for scientific computing](https://software.intel.com/en-us/articles/installing-the-intel-distribution-for-python-and-intel-performance-libraries-with-pip-and) and `tensorflow` (TODO: unfortunately `intel-tensorflow` [see here](https://software.intel.com/en-us/articles/intel-optimization-for-tensorflow-installation-guide#pip_wheels) doesn't seem to work with `intel-numpy`) but [still we can build it somehow (TODO)](https://software.intel.com/en-us/articles/intel-optimization-for-tensorflow-installation-guide#inpage-nav-3).

### Other practical modules

... are listed in `fav-modules.txt` among others (yet to come) [toolz](https://toolz.readthedocs.io) and [funcy](https://funcy.readthedocs.io) for functional data processing and [streaming analytics](https://toolz.readthedocs.io/en/latest/streaming-analytics.html) (`pandas` is sometimes an overkill for a simple `itertools`'s `groupby`).

### Optional

* `pipenv install kaggle` if you want to participate in [kaggle competitions](https://www.kaggle.com/competitions) and setup
* `pipenv install awscli` for AWS