
[![License](http://img.shields.io/:license-affero-blue.svg)](http://www.gnu.org/licenses/agpl-3.0.en.html) [![Build Status](https://travis-ci.org/Malfoy/BWISE.svg?branch=master)](https://travis-ci.org/Malfoy/BGREAT2)

# BGREAT 2

This is a software for mapping sequences to a compacted de Bruijn graph. It is an improved version of [BGREAT](https://github.com/Malfoy/BGREAT). It can be used to know the position of Illumina reads on an assembly graph, or correct the sequencing errors in the graph using read alignments.

# Installation

Type `make`.

# Usage

Input:

-g unitig file (unitig.fa)
-u read file (unpaired)
-x read file (paired)

mandatory arguments:

-k k value (30)

optional arguments:

-m number of missmatch allowed (2)
-t number of thread (1)
-e effort put in mapping (2)
-f path file (paths)
-q for fastq read file
-c to output corrected reads
-O to keep read ordering

# Major changes since version 1

* no longer requires an external tool to align reads on large unitigs
* Better control of memory usage (option `-i 10` will index only 1/10 of the kmers)
* New feature: BGREAT can now be used to correct reads from a DBG (correction mode)

# Correction mode

In correction mode, only unpaired reads can be used, and corrected reads are outputed, if the -O option is used, the corrected reads will be in the right order.
In default mode, the numbers outputed correspond to the paths of unitigs the reads or pair of reads maps on.
>read1
3;4;-6; mean that the read1 mapped on unitig 3 then 4 then the reverse complement of the unitig 6.

To get the corresponding sequence the tool numberToSequences will do the conversion (warning: large file may be produced this way due to redundancy of large unitigs)

usage:
./numbersToSequences  unitigs.fa paths 31 > superReads.fa
