# Overview

Use to search and perform actions on search results.
- It's best to use with text data that has records (rows) and fields
  (columns).

Cheat sheets
- https://quickref.me/awk
- https://gist.github.com/Rafe/3102414

Learning awk
- https://gregable.com/2010/09/why-you-should-know-just-little-awk.html
- https://pmitev.github.io/to-awk-or-not/
- https://ia803404.us.archive.org/0/items/pdfy-MgN0H1joIoDVoIC7/The_AWK_Programming_Language.pdf

User's Guide
- https://www-zeuthen.desy.de/dv/documentation/unixguide/infohtml/gawk/gawk.html

# Samples

```sh
awk -F'\t' '{units_sum[$8]+=$NF}END{for(fc in units_sum)print fc, units_sum[fc]}' prod-available-freight-us.tsv | sort > prod-availalbe-freight-us-sorted.txt

awk -F'\t' '{units_sum[$5]+=$NF}END{for(fc in units_sum)print fc, units_sum[fc]}' gamma-available-freight-us.tsv | sort > gamma-available-group-by-sorted.txt

awk -F, 'NR!=1{fc=$3;units=$NF;units_sum[fc]+=units;for(fc in units_sum){print fc, units_sum[fc]}}' AU-2023-03-29.csv | sort > au.txt

awk -F'\t' '{units_sum[$9]+=$11}END{for(fc in units_sum)print fc, units_sum[fc]}' 1 | sort > us-nti.txt
```
