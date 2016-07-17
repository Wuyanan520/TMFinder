TMFinder
========

Temporal Motif Finder can be used to detect and enumerate motifs in temporal networks. For more information, including the formal definition of temporal networks and temporal motifs as well as the algorithms used, see

TMFinder用来检测和计算时变网络中的模体，包括时变网络、模体的定义和一些算法

> Lauri Kovanen, Márton Karsai, Kimmo Kaski, János Kertész, Jari
Saramäki, "Temporal motifs in time-dependent networks",
Journal of Statistical Mechanics: Theory and Experiments. P11005 (2011)
doi:10.1088/1742-5468/2011/11/P11005

The code also implements the null model for identifying differences between different node and event types. This null model was introduced in

实现了用零模型来检查节点和事件类型的不同

> Lauri Kovanen, Kimmo Kaski, János Kertész, Jari Saramäki. "Temporal motifs reveal homophily, gender-specific patterns and group talk in mobile communication networks." Proceedings of the National Academy of Sciences, 201307941 (2013). doi:10.1073/pnas.1307941110

If you use this code in scientific work, please cite the above publication.

TMFinder is published under the GPL v3 licence.

Installation
------------

TMFinder uses [bliss][bliss] to calculate canonical forms of graphs. You need to install bliss separately to use TMFinder:

1. [Download bliss][bliss] (version 0.72 should work) and compile it by
	following the instructions included with it. Make sure to compile the version without GMP, by calling `make` instead of `make gmp`.

2. Add the path of the bliss directory to the environment variables
	`LIBRARY_PATH` and `CPLUS_INCLUDE_PATH`.

You should now be able to compile TMFinder by calling `make` in the directory `src`. If you get an error message about `bliss` or `graph.hh`, recheck your installation of bliss and the environment variables pointing to the location of the bliss library.

After the compiling, make sure everything works by running the test script `tests/test_small.sh`. This should produce a single output file, `test_small_output.dat` that contains information about the temporal motifs in the small test data.

Python code for handling temporal motifs
----------------------------------------

The `python` subdirectory contains python scripts that should prove useful for analysing and visualizing temporal motifs in the output file. The code relies on PyBliss for calculating graph isomorphisms.

1. [Download and install PyBliss][bliss], the Python wrapper for bliss.
  	PyBliss uses version 0.50 of bliss (this comes with the PyBliss
 	package).

2. Add the path to your PyBliss directory to the environment
   variable PYTHONPATH (both to the root directory containing the file `PyBliss.py` and to subdirectory `lib64/python/`).

The scripts also require a number of other Python libraries that also need to be installed: `pylab`, `numpy`, `pygraphviz` and `argparse`. Make sure these are all installed.

Finally, to make sure everything works run `tests/test_plotting.sh`. This script reads the output of `tests/test_small.sh` and visualizes the detected motifs.

Usage instructions
------------------

For documentation about input and output file formats and usage options, call `bin/tmf --help`. The test scripts should also provide an example for getting started.


Making sense of the output format
---------------------------------

Each line in the output file describes the statistics for one motif, and the motif itself is given at the end of the line as `N [node:color ...] edges ...`.

In this raw output both events and vertices of the original data are represented as nodes; the number in column `N` corresponds to the total number of events and vertices. The word "color" is just another word for type, which here is either event type or vertex type. Color 1 is the default type for events in case event types are not given in the input data. ("Color" is commonly used in the context of identifying canonical forms of graphs, which is one step in identifying temporal motifs.)

For example, `[0:1 1:2 2:3] 0,2 1,0` means graph `[1] -> [0] -> [2]`, but since we know that node 0 is an event (because it has type 1), this means a single event (of type 1) from a node of type 2 to a node of type 3. For more complicated motifs it gets tedious to understand what kind of motif the line represents without making a drawing, and this is why the python plotting library is also included.

For a thorough discussion of the concepts and algorithms, please see sections 1, 2 and 3 in [this article](http://iopscience.iop.org/1742-5468/2011/11/P11005 "Temporal motifs in time-dependent networks"). Figure 2 explains the mapping of events to nodes and why it is needed.


[bliss]: http://www.tcs.hut.fi/Software/bliss/ "bliss"
