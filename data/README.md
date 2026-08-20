# data/

- **`processed/`** — Derived data files used as inputs across multiple analysis scripts (e.g. `treeexp_LA_TPM_gt1_all_species.txt`, the filtered TPM matrix used by the bootstrap tree and relative-rate tests).
- **`annotations/`** — Gene/functional annotation reference files (FlyBase gene sets, GO term lists, etc.) used as candidate groups in the functional-group relative-rate analyses. See [`annotations/README.md`](annotations/README.md).

Raw count data is not stored in this repository; see the `count_dir` parameter in the `01_deseq2_pairwise_*.Rmd` scripts for the expected external location.
