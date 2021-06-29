Testing the effectiveness of **sorted** vs **unsorted** list of integers for BitSet.

This experiment was for comparing performance between:
1. Read graph edges to **sorted bitset** based DiGraph & transpose.
2. Read graph edges to **unsorted bitset** based DiGraph & transpose.

Each approach was attempted on a number of temporal graphs, running each with
multiple batch sizes (`1`, `5`, `10`, `50`, ...). Each batch size was run with 5
different updates to graph, and each specific update was run 5 times for each
approach to get a good time measure. **Transpose** of DiGraph based on
**sorted bitset** is clearly **faster** than the *unsorted* one. However, with
**reading graph edges** there is no clear winner (sometimes *sorted* is
*faster* especially for large graphs, and sometimes *unsorted*). Maybe when
new edges have many duplicates, **inserts are less**, and hence sorted version
is faster (since sorted bitset has slow insert time).

All outputs are saved in [out](out/) and a small part of the output is listed
here. Some [charts] are also included below, generated from [sheets]. The input
data used for this experiment is available at the
[Stanford Large Network Dataset Collection].

<br>

```bash
$ g++ -O3 main.cxx
$ ./a.out ~/data/email-Eu-core-temporal.txt
$ ./a.out ~/data/CollegeMsg.txt
$ ...

# ...
#
# Using graph /home/subhajit/data/sx-stackoverflow.txt ...
# Temporal edges: 63497051
#
# order: 273 size: 901 {} [00025.994 ms] readSnapTemporal [sorted]
# order: 273 size: 901 {} [00025.845 ms] readSnapTemporal [unsorted]
# order: 273 size: 901 {} [00031.129 ms] transposeWithDegree [sorted]
# order: 273 size: 901 {} [00031.053 ms] transposeWithDegree [unsorted]
# order: 870 size: 4447 {} [00034.784 ms] readSnapTemporal [sorted]
# order: 870 size: 4447 {} [00034.335 ms] readSnapTemporal [unsorted]
# order: 870 size: 4447 {} [00048.396 ms] transposeWithDegree [sorted]
# order: 870 size: 4447 {} [00046.927 ms] transposeWithDegree [unsorted]
# order: 1505 size: 8953 {} [00038.823 ms] readSnapTemporal [sorted]
# order: 1505 size: 8953 {} [00038.643 ms] readSnapTemporal [unsorted]
# order: 1505 size: 8953 {} [00048.751 ms] transposeWithDegree [sorted]
# order: 1505 size: 8953 {} [00047.229 ms] transposeWithDegree [unsorted]
# order: 7876 size: 46291 {} [00113.020 ms] readSnapTemporal [sorted]
# order: 7876 size: 46291 {} [00112.610 ms] readSnapTemporal [unsorted]
# order: 7876 size: 46291 {} [00109.025 ms] transposeWithDegree [sorted]
# order: 7876 size: 46291 {} [00105.595 ms] transposeWithDegree [unsorted]
# order: 11713 size: 92953 {} [00161.687 ms] readSnapTemporal [sorted]
# order: 11713 size: 92953 {} [00159.737 ms] readSnapTemporal [unsorted]
# order: 11713 size: 92953 {} [00119.197 ms] transposeWithDegree [sorted]
# order: 11713 size: 92953 {} [00113.941 ms] transposeWithDegree [unsorted]
# order: 38489 size: 456121 {} [00568.842 ms] readSnapTemporal [sorted]
# order: 38489 size: 456121 {} [00563.231 ms] readSnapTemporal [unsorted]
# order: 38489 size: 456121 {} [00197.264 ms] transposeWithDegree [sorted]
# order: 38489 size: 456121 {} [00170.921 ms] transposeWithDegree [unsorted]
# order: 79767 size: 907368 {} [01124.046 ms] readSnapTemporal [sorted]
# order: 79767 size: 907368 {} [01066.157 ms] readSnapTemporal [unsorted]
# order: 79767 size: 907368 {} [00311.044 ms] transposeWithDegree [sorted]
# order: 79767 size: 907368 {} [00262.041 ms] transposeWithDegree [unsorted]
# order: 574600 size: 4532366 {} [05601.660 ms] readSnapTemporal [sorted]
# order: 574600 size: 4532366 {} [05480.637 ms] readSnapTemporal [unsorted]
# order: 574600 size: 4532366 {} [01903.864 ms] transposeWithDegree [sorted]
# order: 574600 size: 4532366 {} [01584.327 ms] transposeWithDegree [unsorted]
# order: 1256732 size: 9107956 {} [11860.497 ms] readSnapTemporal [sorted]
# order: 1256732 size: 9107956 {} [11389.886 ms] readSnapTemporal [unsorted]
# order: 1256732 size: 9107956 {} [05179.272 ms] transposeWithDegree [sorted]
# order: 1256732 size: 9107956 {} [04580.456 ms] transposeWithDegree [unsorted]
# order: 2523890 size: 30385833 {} [60537.383 ms] readSnapTemporal [sorted]
# order: 2523890 size: 30385833 {} [57709.414 ms] readSnapTemporal [unsorted]
# order: 2523890 size: 30385833 {} [16493.771 ms] transposeWithDegree [sorted]
# order: 2523890 size: 30385833 {} [18024.605 ms] transposeWithDegree [unsorted]
```

[![](https://i.imgur.com/AO60Lp2.gif)][sheets]

<br>
<br>


## References

- [Stanford Large Network Dataset Collection]

<br>
<br>

[![](https://i.imgur.com/DuJu78s.jpg)](https://www.youtube.com/watch?v=2k_ihEEZG-o)

[Stanford Large Network Dataset Collection]: http://snap.stanford.edu/data/index.html
[charts]: https://photos.app.goo.gl/c2ivFPbEXdw6ZFaM7
[sheets]: https://docs.google.com/spreadsheets/d/1AB23nO5K71-TWe7aY6cf5Rte7jfLhfITPFBnRB_jVzM/edit?usp=sharing
