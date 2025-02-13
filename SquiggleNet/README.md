# Quick Start Guide for SquiggleNet Docker Image

This Docker image provides a quick and easy way to utilize the `SquiggleNet` bioinformatics tool, designed to classify raw nanopore signals as target or non-target for Read-Until sequence enrichment or depletion. The image encapsulates the tool and its dependencies, simplifying setup and usage for end users. This image is maintained independently and is not an official release from the developers of `SquiggleNet`.

## Upstream Repository

For comprehensive documentation, feature requests, or to report issues, please refer to the main SquiggleNet repository at:
[SquiggleNet on GitHub](https://github.com/welch-lab/SquiggleNet)

## Usage Instructions

To use `SquiggleNet` via Docker, you can set an alias as follows. 

```bash
alias squigglenet="docker run --rm -it -v $PWD:/workspace squigglenet"
```

### Basic Examples

1. **Classification**

	The SquiggleNet authors provide two pretrained models:
	- `model_B4_2_3000_totmad_br_2.ckpt` - trained on Human&Zymo_b12
	- `model_B4t2_3000_tot32.ckpt` - trained on HeLa&Zymo
	These can be used out-of-the-box to perform nanopore raw signal classification. In case these models are not suitable, a custom model can be trained.
	
	The following command performs binary classification using one of the pretrained models.
	```bash
	squigglenet inference.py -m /app/SquiggleNet/models/model_B4_2_3000_totmad_br_2.ckpt -i /workspace/nanopore_fast5s -o /workspace/squigglenet_results`
	```
	The command needs to be executed from the root directory containing your nanopore data, because this is the directory that will be mounted to the containers `/workspace`.
	
2. **Training a custom model:**

	Under construction.

## Warnings and Precautions

- **Mounting Volumes:** When running the Docker command, ensure that your current working directory (`$PWD`) is mounted correctly to `/workspace` in the container. This setup is crucial for the tool to access data files on your local system.
- **GPU:** SquiggleNet is able to run on GPU, but this is currently not supported by this Docker image.
