
.. image:: https://img.shields.io/appveyor/ci/laurentnoe/iedera/badges.svg?style=flat-square&label=AppVeyor%20CI
    :target: https://ci.appveyor.com/project/laurentnoe/iedera/badges
    :alt: Build Status Windows

.. image:: https://img.shields.io/travis/laurentnoe/iedera/badges.svg?style=flat-square&label=Travis%20CI
    :target: https://travis-ci.org/laurentnoe/iedera/badges
    :alt: Build Status Unix

..  imagehttps://img.shields.io/coveralls/laurentnoe/iedera/master.svg?style=flat-square&label=Coveralls
    targethttps://coveralls.io/github/laurentnoe/iedera
    altCoverage Status

.. imagehttps://img.shields.io/pypi/v/appveyor-artifacts.svg?style=flat-square&label=Latest
   targethttps://pypi.python.org/pypi/appveyor-artifacts
   altLatest Version

.. imagehttps://img.shields.io/pypi/dm/appveyor-artifacts.svg?style=flat-square&label=PyPI%20Downloads
   targethttps://pypi.python.org/pypi/appveyor-artifacts
   altDownloads

iedera
======

(more at  http://bioinfo.lifl.fr/yass/iedera.php)

``iedera`` is a tool to select and design *spaced seeds*, *transition
constrained spaced seeds*, or more generally *subset seeds*, and
*vectorized subset seed* patterns.


Installation
------------

(more at  http://bioinfo.lifl.fr/yass/iedera.php#downloadiedera)

You need a C++ compiler and the autotools. On Linux, you can install
``g++``, ``autoconf``, ``automake``. On Mac, you can install
``xcode``, or the command line developer tools (or you can use
``macports`` to install ``g++-mp-5`` for example).


Using the command line, type::

  git clone https://github.com/laurentnoe/iedera.git
  cd iedera
  ./configure
  make

or::
  
  git clone https://github.com/laurentnoe/iedera.git
  cd iedera
  autoreconf
  ./configure
  automake
  make

you can install  ``iedera`` to a standard ``/local/bin`` directory::

  sudo make install

or copy the binary directly to your homedir::
   
  cp iedera ~/.

Command-line
------------

(more at  http://bioinfo.lifl.fr/yass/iedera.php#quick)


**First, use** one of these two parameters :
 
-spaced
  for spaced seeds

-transitive
  for transitive spaced seeds

since they are **shortcuts for quite long command lines**.


 
Then you can change the weight, span, and number of seeds being
designed:
 
-w <N,N>
  for the weight range, where *N = [1..16]* seems reasonable

-s <N,N>
  for the span range, where *N = [1..32]* seems reasonable
 
-n <N>
  for the number of seeds, where *N = [1..32]*



as well as the length of the alignment:

-l <N>
  where *N = [1..64]*  seems reasonable


``NOTE :``
since enumeration of ``all the combination of multiple seeds`` may
take time, if "-n" is chosen with a value greater than one, please
consider the two following:


-r <N>
  to run the tool on *N*  randomly generated seed patterns

-k
  to activate the hill-climbing algorithm on previous parameter -r
 

(more at  http://bioinfo.lifl.fr/yass/iedera.php#details)
   
  
Examples
--------

Spaced seeds
~~~~~~~~~~~~
  
A very small example where the weight is set to 11 and span at most 22 (full enumeration)::

  iedera -spaced -w 11,11 -s 11,22

A second example where the number of seeds is now set to 2, alignment length to 50 and 10000 trial will be done with the hill-climbing algorithm::

  iedera -spaced -n 2 -w 11,11 -s 11,22 -l 50 -r 10000 -k


Transition seeds
~~~~~~~~~~~~~~~~

A very small example for transition seeds (hill climbing)::

  iedera -transitive -w 11,11 -s 11,22 -r 10000 -k



Lossless seeds
~~~~~~~~~~~~~~

A very small example for lossless seeds (from Burkhard&Karkkainen) : find a *lossless seed* of weight 12, span at most 19, on alignments of length 25 with 2 mismatches::

  
  iedera -spaced -s 12,19 -w 12,12 -l 25 -L 1,0 -X 2


A second example for lossless seeds (from Kucherov,Noe&Roytberg) on the previous problem, but with two seeds of weight 14, and span between 20 and 21 (to ease the search)::


  iedera -spaced -l 25 -L 1,0 -X 2 -n 2 -s 20,21 -w 14,14  -r 100..some.zeros..00 -k
  
