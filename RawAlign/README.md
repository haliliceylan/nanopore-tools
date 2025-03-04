# Quick Start Guide for RawAlign Docker Image

This Docker image provides a quick and easy way to utilize the `RawAlign` bioinformatics tool, designed to facilitate efficient alignment of raw nanopore signals. The image encapsulates the tool and its dependencies, simplifying setup and usage for end users. It's important to note that this image is maintained independently and is not an official release from the developers of `RawAlign`.

## Upstream Repository

For comprehensive documentation, feature requests, or to report issues, please refer to the main RawAlign repository at:
[RawAlign on GitHub](https://github.com/cmu-safari/RawAlign)

## Usage Instructions

To use `RawAlign` via Docker, you can set an alias as follows. This alias will help in running the `RawAlign` commands inside a Docker container, making the process seamless:

```bash
alias rawalign="docker run --rm -it -v $PWD:/workspace haliliceylanua/rawalign:latest rawalign"
```

### Basic Examples

1. **Indexing (make an index file from a reference genome in FASTA format)**
   ```bash
   rawalign -d ref.ind -p /extern/local_kmer_models/r10_180mv_450bps_9mer/template_r10_9mer.model -t 32 reference.fasta
   ```

2. **Mapping (Dynamic Time Warping (DTW) Chain Evaluation):**
   ```bash
   rawalign --dtw-evaluate-chains -t 32 -x sensitive ref.ind <fast5_filename>.fast5 > mapping.paf
   ```

### Model Files

The Docker image includes several pre-installed k-mer model files, which are critical for the DNA alignment process. These models can be found in the `/extern/` directory:

- **R9.2 Models:**
  ```
  /extern/kmer_models/r9.2_180mv_250bps_6mer/complement_median68pA_pop1.model
  /extern/kmer_models/r9.2_180mv_250bps_6mer/complement_median68pA_pop2.model
  /extern/kmer_models/r9.2_180mv_250bps_6mer/template_median68pA.model
  ```

- **R9.4 Models:**
  ```
  /extern/kmer_models/r9.4_180mv_450bps_6mer/template_median68pA.model
  /extern/kmer_models/r9.4_180mv_70bps_5mer_RNA/template_median69pA.model
  /extern/kmer_models/r9.4_200mv_70bps_5mer_RNA/template_median68pA.model
  ```

- **R10 Models:**
  ```
  /extern/local_kmer_models/r10_180mv_450bps_9mer/template_r10_9mer.model
  ```
  
## Warnings and Precautions

- **Mounting Volumes:** When running the Docker command, ensure that your current working directory (`$PWD`) is mounted correctly to `/workspace` in the container. This setup is crucial for the tool to access data files on your local system.
- **Concurrency:** Usage of the `-t` option sets the number of threads. Make sure your system can handle the concurrency level you specify.
