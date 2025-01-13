# Quick Start Guide for Sigmoni Docker Image

This Docker image provides a quick and easy way to utilize the `Sigmoni` bioinformatics tool, designed to rapidly classify raw nanopore signals. The image encapsulates the tool and its dependencies, simplifying setup and usage for end users. This image is maintained independently and is not an official release from the developers of `Sigmoni`.

## Upstream Repository

For comprehensive documentation, feature requests, or to report issues, please refer to the main Sigmoni repository at:
[Sigmoni on GitHub](https://github.com/vikshiv/sigmoni)

## Usage Instructions

To use `Sigmoni` via Docker, you can set an alias as follows. This alias will help in running the `Sigmoni` commands inside a Docker container, making the process seamless:

```bash
alias sigmoni="docker run --rm -it -v $PWD:/workspace haliliceylanua/sigmoni:latest"
```

### Basic Examples

1. **Indexing (make an index file from the reference genomes in FASTA format)**
   Before read classification can be performed, an index needs to be built over the reference. This process is different depending on the mode that will be used during classification (i.e. multi-class or binary). To enable multi-class classification, multiple references need to be provided:
   ```bash
   sigmoni python3 /sigmoni/index.py -p ./data/ref_genomes/*.fasta --shred 100000 -o ./sigmoni --ref-prefix refgenome_sigmoni
   ```
   To enable binary classification, positive and null references need to be provided:
   ```bash
   sigmoni python3 /sigmoni/index.py -p ./data/positive_ref_genome/*.fasta -n ./data/null_ref_genome/*.fasta --shred 100000 -o ./sigmoni --ref-prefix refgenome_sigmoni
   ```
   These commands will create a set of index files, which can be found in `./sigmoni/refs`. The `--shred` option can be used to control the location resolution of the mapping. The default shred size is 100 kpb. Decreasing the shred size will increase the overall index size, but provide finer grain locality information.

2. **Classification (binary or multi-class, using the r-index and a signal binning procedure):**
   To perform multi-class classification, the `--multi` flag needs to be provided. Each read will be classified as belonging to one of the indexed references.
   ```bash
   sigmoni python3 /sigmoni/main.py -i ./data/fast5 -r ./sigmoni/refs/refgenome_sigmoni -o ./sigmoni -t 48 --sp --multi
   ```
   To perform binary classification, either a threshold needs to be provided, or the default threshold will be used.

### Output

1. `*.report` file, listing the classification for each read
2. `*.pseudo_lengths` file, listing the PML profile for each read
  
## Warnings and Precautions

- **Mounting Volumes:** When running the Docker command, ensure that your current working directory (`$PWD`) is mounted correctly to `/workspace` in the container. This setup is crucial for the tool to access data files on your local system.
- **Concurrency:** Usage of the `-t` option sets the number of threads. Make sure your system can handle the concurrency level you specify.
