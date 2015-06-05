# Introduction #

Junto provides an implementation several label propagation algorithms, including, Adsorption and Modified Adsorption (MAD).

This page is a rough draft of notes on using Junto.


# Obtaining and Building Junto #

The version of Junto relevant for this page is not released yet. You can get the code from the Mercurial repository:

```
hg clone https://junto.googlecode.com/hg/ junto
```

Then, follow the instructions in the `README` file to get Junto compiled and test whether it is working on the simple example graph.

# Running Label Propagation #

Look at `junto/examples/simple/simple_config` and the instructions contained in that file to see how to set up and configure the options for Junto.

Once you have your config file and graph data prepared, run label propagation:

```
junto config <configfile>
```


# Running the output extractor #

Junto output files contain information about the distributions found for each node, plus information about gold labels, seeds, and more. If all you want are distributions for a particular type, the extractor can conveniently pull these out for you.

The extractor assumes that the nodes are named with the pattern `TYPE_NODEID`, eg. `WORD_the`  and `CAT_NP`. If you want the distributions for all WORD types, you can then do:

```
junto extract -t WORD <outputfile>
```

The distributions also include the DUMMY label, and often one just wants the labels that have higher probability than the DUMMY. So, if you want only those labels, add the option `-d`:

```
junto extract -d -t WORD <outputfile>
```

This will also renormalize the probabilities for those labels, such that the normalization is the sum of the probabilities of all labels above DUMMY.