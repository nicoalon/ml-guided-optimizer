# Ml-guided-optimizer

This repository contains a series of csv in wich we have included the blocks used to train and evaluate the models.

Additionally, you can use our tool by using our Docker image.


## Prerequisites

*   [Docker](https://docs.docker.com/get-docker/) installed on your machine.

## Getting Started

### 1. Pull the Image
If you are using the image hosted on Docker Hub:
```bash
docker pull nicoalon/ml-guided-optimizer:v1.1
```

### 2. Basic Usage (Manual Mode)
The docker image allready contains the block used as the running example in our paper and it will be used by default. However you can run the optimizer on a local file.
To run the optimizer using a local file, you must mount your local directory to the `/data` folder inside the container using the `-v` flag.

```bash
docker run --rm -v "$(pwd):/data" nicoalon/ml-guided-optimizer:v1.1 -bl /data/block.txt
```
*By default, this uses the `original` optimization strategy.*

### 3. ML-Guided Mode
If you want the tool to automatically decide the best optimization strategy using Machine Learning:

```bash
docker run --rm -v "$(pwd):/data" nicoalon/ml-guided-optimizer:v1.1 -bl /data/block.txt --ml-guided
```

---

## Available Options

| Option | Values | Description |
| :--- | :--- | :--- |
| `-bl`, `--block-file` | `[path]` | Path to your input block file. |
| `--ml-guided` | | Activates ML-based optimization (overrides manual settings). |
| `--split-location` | `first`, `middle`, `last` | Where to perform the split (Default: `first`). |
| `--split-strategy` | `simple-cp`, `simple-sat`, `minimal-cp`, `minimal-sat`, `original` | Optimization strategy (Default: `original`). |
| `--traversal-strategy` | `seq`, `sdg` | Traversal strategy (Default: `seq`). |
| `--compiler` | `v0_8_24`, `v0_8_30` | The compiler used to obtain the block (Default: `v0_8_24`). |

### Example with custom parameters:
```bash
docker run --rm -v "$(pwd):/data" nicoalon/ml-guided-optimizer:v1.1 \
  -bl /data/block.txt \
  --split-strategy simple-cp \
  --split-location first \
```

---

## Troubleshooting

*   **Permission Denied:** If you are on Linux, you might need to run docker with `sudo` or ensure your user is in the `docker` group.
