# Research-Project-Brain-Evolution

MSc research project analysing *Drosophila* larvae transcriptomic divergence across six species — *D. melanogaster*, *D. simulans*, *D. sechellia*, *D. santomea*, *D. erecta*, and *D. suzukii* — with a focus on gene-expression evolution in the nervous system.

## Pipeline

Each species-comparison folder runs the same numbered pipeline:

1. **`01_deseq2_pairwise_*.Rmd`** — Pairwise DESeq2 differential expression between the focal species and each other species in the panel.
2. **`02_go_enrichment_*.Rmd`** — GO term enrichment on the differentially expressed gene sets.
3. **`03_bootstrap_transcriptomic_tree.Rmd`** — Builds a bootstrapped whole-transcriptome expression tree (100 replicates) from filtered TPM data.
4. **`04_whole_transcriptome_relative_rate*.Rmd`** — Relative-rate tests for whole-transcriptome expression divergence, using *D. suzukii* as the outgroup/reference.
5. **`05_*_relative_rate.Rmd`** / **`06_*_relative_rate.Rmd`** — Independent relative-rate analyses restricted to FlyBase functional gene groups (e.g. neuropeptides, transcription factors, nervous system process genes), comparing the focal species against specific ingroup/outgroup combinations.

Each `.Rmd` knits to a self-contained `.html` report with the same name.

## Repository structure

```
erecta/     Pipeline outputs and scripts for the D. erecta comparisons (vs mel, san, sec, sim, suz)
simulans/   Pipeline outputs and scripts for the D. simulans comparisons (vs mel, sec, sim... )
```

The candidate FlyBase gene-set files used in the functional-group relative-rate analyses (neuropeptides, transcription factors, GO process terms such as cellular respiration, chitin binding, cuticle development, molting cycle, nervous system, etc.) are read from an external path (see `params` in the `05_*`/`06_*` `.Rmd` files) and are not stored in this repository.

Within each species folder:
- `DESeq2_D**_vs_D**.csv` — pairwise DESeq2 results
- `normalized_counts_all_species2.csv` — normalized count matrix used across the pipeline
- `deseq2_GO_input_objects.rds` — saved R objects feeding the GO enrichment step
- `treeexp_LA_TPM_gt1_all_species.txt` (simulans) — filtered TPM matrix (TPM > 1) used for the tree and relative-rate tests

## Notes

- All relative-rate results assume the outgroup species is an unbiased neutral reference; see the caveats noted in `04_whole_transcriptome_relative_rate_SIM.Rmd` regarding potential long-branch-attraction-like bias.
- Reports are written with `rmarkdown::render()`; params at the top of each `.Rmd` control input file paths, bootstrap replicate counts, and comparison species.
