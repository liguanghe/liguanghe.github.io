---
title: Mac can't import matplotlib?
date: 2017/11/11 16:45:32
categories: 
- python


tags: 
- python
- Record
- bug
- solve

---

## Problem

```
>>> import matplotlib.pyplot as plt
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/matplotlib/pyplot.py", line 115, in <module>
    _backend_mod, new_figure_manager, draw_if_interactive, _show = pylab_setup()
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/matplotlib/backends/__init__.py", line 32, in pylab_setup
    globals(),locals(),[backend_name],0)
  File "/Users/liguanghe/.pyenv/versions/3.6.1/lib/python3.6/site-packages/matplotlib/backends/backend_macosx.py", line 19, in <module>
    from matplotlib.backends import _macosx
RuntimeError: Python is not installed as a framework. The Mac OS X backend will not be able to function correctly if Python is not installed as a framework. See the Python documentation for more information on installing Python as a framework on Mac OS X. Please either reinstall Python as a framework, or try one of the other backends. If you are using (Ana)Conda please install python.app and replace the use of 'python' with 'pythonw'. See 'Working with Matplotlib on OSX' in the Matplotlib FAQ for more information.

```

## Solution
```
$ cd .matplotlib
.matplotlib liguanghe$ echo 'backend: TkAgg' > matplotlibrc
.matplotlib liguanghe$ ls
fontList.py3k.cache	matplotlibrc		tex.cache
```

## Relevance

- [osx - Installation Issue with matplotlib Python - Stack Overflow](https://stackoverflow.com/questions/21784641/installation-issue-with-matplotlib-python)
