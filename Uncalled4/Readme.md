# Quick Start Guide for the UNCALLED4 Docker Image

This Docker image provides a quick and easy way to utilize the `UNCALLED4` bioinformatics tool, designed to facilitate basecaller-guided nanopore signal alignment. The image encapsulates the tool and its dependencies, simplifying setup and usage for end users. It's important to note that this image is maintained independently and is not an official release from the developers of `UNCALLED4`.

## Upstream Repository

For comprehensive documentation, feature requests, or to report issues, please refer to the main UNCALLED4 repository at:
[UNCALLED4 on GitHub](https://github.com/skovaka/uncalled4)

## Usage Instructions

To use `UNCALLED4` via Docker, you can set an alias as follows. This alias will help in running the `UNCALLED4` commands inside a Docker container, making the process seamless:

```bash
alias uncalled4="docker run --rm -it -v $PWD:/workspace haliliceylanua/uncalled4:latest"
```

### Basic Examples

1. **Align raw nanopore signals in the current directory to a reference genome given mapped basecalled reads**
   ```bash
   uncalled4 align reference.fasta ./ --bam-in calls.sam --bam-out signal_aln.bam
   ```

2. **Generate a trackplot:**
   ```bash
   uncalled4 trackplot --ref_index reference.fasta chr:start-end signal_aln.bam
   ```
  
## Warnings and Precautions

- **Mounting Volumes:** When running the Docker command, ensure that your current working directory (`$PWD`) is mounted correctly to `/workspace` in the container. This setup is crucial for the tool to access data files on your local system.
- **Concurrency:** Usage of the `-t` option sets the number of threads. Make sure your system can handle the concurrency level you specify.
