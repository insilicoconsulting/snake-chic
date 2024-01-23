# Snakemake wrapper for the Arima Capture HiC (CHiC) workflow

This is a simple [Snakemake](https://snakemake.github.io/) wrapper around the [Arima Genomics Capture Hi-C (CHiC) workflow](https://github.com/ArimaGenomics/CHiC).
This wrapper allows the Arima workflow to be executed in parallel and with a reproducible Conda environment.
Software versions used by this wrapper versus the ones mentioned in the Arima workflow differ, since the Arima versions are quite old and require manual installation.
Software versions were chosen to be compatible with the ones validated by Arima.

## Installation

1. Install the [Miniconda software distribution](https://docs.conda.io/projects/miniconda/en/latest) at a convenient location.
2. Add the [Bioconda](https://bioconda.github.io) software channel, as [described](https://bioconda.github.io/#usage).
3. Install Snakemake, e.g. in a new conda environment: `conda create -n snakemake snakemake`
4. Check out the Arima workflow repository: `git clone https://github.com/ArimaGenomics/CHiC.git arima-chic`
5. In the `arima-chic` directory above, uncompress the `chicagoTools.tar.gz` file: `tar xvf chicagoTools.tar.gz`, resulting in a `arima-chic/chicagoTools` directory.
6. Check out the `snake-chic` repository: `git clone https://github.com/insilicoconsulting/snake-chic snake-chic`

## Usage

The workflow expects paired-end FASTQ files in the directory `fastq`, relative to the `snake-chic` directory containing the workflow.
The files must be named in the format `samplename_[R1|R2].fastq.gz`, e.g. `sample1_R1.fastq.gz` and `sample1_R2.fastq.gz`.
It's probably easiest to create this naming format using symbolic links, e.g. `ln -s /datadir/sample1_S1_L001_R1_001.fastq.gz fastq/sample1_R1.fastq.gz`.

- Adapt the parameters in `config/config.yaml` to the requirements. Adapt the `arima_dir` parameter to the location of the `arima-chic` workflow directory above, and the `chicago_dir` parameter to the location of the `chicagoTools` directory above. The other parameters are explained in the [Arima repository README file](https://github.com/ArimaGenomics/CHiC).
- Activate the `snakemake` Conda environment: `conda activate snakemake`
- Execute the workflow: `snakemake --use-conda -p --cores 16`
