[![Build Status](https://travis-ci.org/dpryan79/libGTF.svg?branch=master)](https://travis-ci.org/dpryan79/libGTF)

libGTF a library for parsing/searching GTF and BED files
========================================================

Note that this library is not yet appropriate for real-world use (the documentation hasn't even been written yet!).

In essense, this library construct an interval tree representation of GTF or BED files and allows overlap searches, similar to GenomicRanges or bedtools. The primary difference here is the convenient C interface that allows incorporation into other programs easily.

Note that murmur3.c and murmur3.h are C implementations of MurmurHash. The C implementation is from [Peter Scott](https://github.com/PeterScott/murmur3) and MurmurHash itself is by [Austin Appleby](https://code.google.com/p/smhasher/wiki/MurmurHash3). Both of these are in the public domain.

Installation
============

    git clone https://github.com/dpryan79/libGTF.git
    git submodule init
    git submodule update
    make

Examples
========

There are currently a few example programs in the `tests/` directory.

  * `testBED` demonstrates how to parse a BED file and display its tree representation in dot format.
  * `testGTF` is the equivalent program for GTF files.
  * `testFindOverlaps` demonstrates how to find overlaps of alignments in SAM/BAM/CRAM format with a GTF file. This is largely similar to featureCounts and htseq-count, though this program doesn't handle paired-end alignments intelligently (it is, afterall, just a demonstration). The code demonstrates processing sets of overlaps and merging them for further processing. This program also demonstrates how to use different match and strand types. Note that in a real program, it'd be simpler to use the `findOverlapsBAM()` function.
  * `testCountOverlaps` demonstrates how to count the number of overlapping elements per alignment. Note that there's no method to filter this, for example, to only count the number of exonic overlaps. For such purposes, it's better to use the findOverlaps() function and filter the results.
  * `testOverlapsAny` is similar to `testCountOverlaps`, but simply returns a binary 0 or 1, indicating whether there's at least a single overlap.
  * The aforementioned programs also demonstrate how one can use filter functions, both when parsing a GTF file and when traversing one.

To Do
=====

 - [ ] compare with featureCounts/bedtools and ensure the results are the same
