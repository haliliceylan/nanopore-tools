# Quick Start Guide for RawAlign Docker Image

This Docker image provides a quick and easy way to utilize the `RawAlign` bioinformatics tool, designed to facilitate efficient DNA alignment. The image encapsulates the tool and its dependencies, simplifying setup and usage for end users. It's important to note that this image is maintained independently and is not an official release from the developers of `RawAlign`.

## Upstream Repository

For comprehensive documentation, feature requests, or to report issues, please refer to the main RawAlign repository at:
[RawAlign on GitHub](https://github.com/cmu-safari/RawAlign)

## Usage Instructions

To use `RawAlign` via Docker, you can set an alias as follows. This alias will help in running the `RawAlign` commands inside a Docker container, making the process seamless:

```bash
alias rawalign="docker run --rm -it -v $PWD:/workspace haliliceylanua/rawalign"
```

### Basic Examples

1. **Simple DNA Alignment:**
   ```bash
   rawalign -d ref.ind -p /extern/local_kmer_models/r10_180mv_450bps_9mer/template_r10_9mer.model -t 32 chikV1.fasta
   ```

2. **Dynamic Time Warping (DTW) Chain Evaluation:**
   ```bash
   rawalign --dtw-evaluate-chains -t 32 -x sensitive ref.ind CHIKV-1.pod5_1.0_0.fast5 > mapping.paf
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

## Warnings and Precautions

- **Mounting Volumes:** When running the Docker command, ensure that your current working directory (`$PWD`) is mounted correctly to `/workspace` in the container. This setup is crucial for the tool to access data files on your local system.
- **Concurrency:** Usage of the `-t` option sets the number of threads. Make sure your system can handle the concurrency level you specify.

## Further Assistance

For additional support or if you have questions regarding the usage of this Docker image, please refer to the [main RawAlign repository](https://github.com/cmu-safari/RawAlign).