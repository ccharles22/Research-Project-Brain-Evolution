# Research-Project-Brain-Evolution

MSc research project analysing *Drosophila* larvae transcriptomic divergence across six species — *D. melanogaster*, *D. simulans*, *D. sechellia*, *D. santomea*, *D. erecta*, and *D. suzukii* — with a focus on gene-expression evolution in the nervous system.

## Pipeline

Each species runs the same numbered pipeline, with the tree-building step shared across species:

1. **`analysis/*/01_deseq2_pairwise_*.Rmd`** — Pairwise DESeq2 differential expression between the focal species and each other species in the panel.
2. **`analysis/*/02_go_enrichment_*.Rmd`** — GO term enrichment on the differentially expressed gene sets.
3. **`analysis/shared/03_bootstrap_transcriptomic_tree.Rmd`** — Builds a bootstrapped whole-transcriptome expression tree (100 replicates) from filtered TPM data. Shared by both species, since the underlying tree isn't species-specific.
4. **`analysis/*/04_whole_transcriptome_relative_rate*.Rmd`** — Relative-rate tests for whole-transcriptome expression divergence, using *D. suzukii* as the outgroup/reference.
5. **`analysis/*/05_functional_groups_relative_rate_*.Rmd`** / **`analysis/erecta/06_functional_groups_relative_rate_ERE_vs_SAN.Rmd`** — Independent relative-rate analyses restricted to FlyBase functional gene groups (e.g. neuropeptides, transcription factors, nervous system process genes), comparing the focal species against specific ingroup/outgroup combinations.

Each `.Rmd` knits to a self-contained `.html` report of the same name under `htmls/`.

## Repository structure

```
analysis/     .Rmd analysis scripts, organised by species (erecta/, simulans/) plus shared/
data/         Processed/derived inputs (processed/) and annotation reference files (annotations/)
results/      Analysis outputs: DESeq2 tables, count matrices, GO objects, bootstrapped tree outputs
figures/      Plots generated from the analyses, by species
htmls/        Rendered .html reports, mirroring the analysis/ layout
```

- `data/processed/treeexp_LA_TPM_gt1_all_species.txt` — filtered TPM matrix (TPM > 1) shared by the tree-building and relative-rate steps.
- `results/erecta/`, `results/simulans/` — pairwise DESeq2 CSVs, normalized count matrices, and saved GO input objects (`.rds`) per species.
- `results/treeexp/` — output of the bootstrapped tree script.
- `data/annotations/` — see [`data/annotations/README.md`](data/annotations/README.md); candidate gene-set files aren't currently committed here and are read from an external path (see `params` in the `05_*`/`06_*` `.Rmd` files).

## Notes

- All relative-rate results assume the outgroup species is an unbiased neutral reference; see the caveats noted in `analysis/simulans/04_whole_transcriptome_relative_rate_SIM.Rmd` regarding potential long-branch-attraction-like bias.
- Reports are written with `rmarkdown::render()`; params at the top of each `.Rmd` control input file paths, bootstrap replicate counts, and comparison species.
- `renv.lock` is currently a placeholder — run `renv::init()` / `renv::snapshot()` from RStudio to capture actual package versions.
