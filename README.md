<!--
SPDX-FileCopyrightText: 2021 Anders Rune Jensen

SPDX-License-Identifier: CC-BY-4.0
-->

:warning: **This repo was moved to https://github.com/ssbc/db-benchmarks.** This archival will remain in this GitHub org `ssb-ngi-pointer` to demonstrate the outcome of the work done by the SSB NGI Pointer team during 2020 and 2021. The SSB NGI Pointer team is no longer active because we completed our grant project.

# DB benchmark

This repo is meant as a place to track our progress in improving the
performance of the database used for [secure
scuttlebutt](https://github.com/ssbc/).

## Usage

Generate a dataset using [ssb-fixures](https://github.com/ssb-ngi-pointer/ssb-fixtures/) for testing:
```
npm run generate-data
```

This will create a database consisting of 100.000 fake messages,
generated with a realistic distribution of the different kind of
messages types and encrypted messages.

Optional, apply the [aligned-block fix](https://github.com/flumedb/aligned-block-file/pull/11):
```
npm run aligned-block-fix
```

Finally run the benchmark:
```
npm run benchmark
```

On the first run, indexes will be created and this is mainly what we
are interested in testing here. Subsequent will reuse the indexes so
to run the index creating benchmark again, do a:
```
npm run clean-indexes
```

## Results

Comparing [ssb-db](https://github.com/ssbc/ssb-db/) 20.3 against
[ssb-db2](https://github.com/ssb-ngi-pointer/ssb-db2) 0.5.0, using
ssb-fixtures 2.2.0 (no private groups) indexing 10.000 messages:
```
db1: 4.658s
db2: 939.209ms
```
roughly 4.9x speed up

Indexing 100.000 messages:
```
db1: 36.836s
db2: 4.994s
```
roughly 7.3x speed up

Indexing 1.000.000 messages:
```
db1: 4:23.873 (m:ss.mmm)
db2: 26.754s
```
roughly 9.89x speed up
