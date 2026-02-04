# phasing-snakemake

## Installation

1. If you haven't yet, install [conda miniforge](https://github.com/conda-forge/miniforge?tab=readme-ov-file#install).

2. Clone this repository and cd into it:

    ```bash
    git clone https://github.com/gmanthey/phasing-snakemake.git
    cd phasing-snakemake
    ```

3. Create a new environment from the environment specs file:
    ```bash
    conda env create -f environment.yml
    ```

    If the `phasing-snakemake` environment had been created previously, make sure 
    you update to the newest version using `conda env update --file environment.yml --prune`

## Usage

1. Copy the `config.yml.template` file to `config.yml` 
2. Adjust the paths to the vcf file and gmap directory (If you used the [recombination-snakemake](https://github.com/gmanthey/recombination-snakemake) pipeline, this is `<path-to-recombination-snakemake>/results/<population-name>/cM`). Also adjust the mutation rate `mu`, the example provided is used often for songbirds and is based on [Smeds et al. 2016. Direct estimate of the rate of germline mutation in a bird](https://doi.org/10.1101/gr.204669.116).
3. Create the `resources/chromosomes.txt` file, which should contain one line per chromosome and just the name of the chromosome on the line. I have only so far run this with autosomes, presumably sex-chromosomes require additional adjustments.
4. Create the `resources/populations.txt` file, which should contain one line per individual, with the first column containing a population identifier and the second column containing the individual identifier. Different populations will be phased independently. If all individuals are to be phased together, use the same population identifier for all of them.
5. Run the workflow:
   ```bash
   snakemake
   ```
   If you are on Uni Oldenburgs rosa cluster, you may use the `--profile profile/default` flag to set command line options to use the slurm system of that cluster.
