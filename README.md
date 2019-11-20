# Biomedical Jupyter Examples

This repository contains Jupyter Notebooks that resemble the following analysis as a demonstration for reproducible and executable research experiments:

Susanne Staehlke, Henrike Rebl, Birgit Finke, Petra Mueller, Martina Gruening, and J. Barbara Nebe.
“Enhanced calcium ion mobilization in osteoblasts on amino group containing plasma polymer nanolayer.”
Cell & Bioscience, 8(1), March 2018.
doi: 10.1186/s13578-018-0220-8

## License

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/), please use the Zenodo reference:

[![DOI](https://zenodo.org/badge/169142559.svg)](https://zenodo.org/badge/latestdoi/169142559)

In order to reference the GitHub repository, please attribute this as:

Max Schröder, Susanne Staehlke, J. Barbara Nebe, and Frank Krüger. “Biomedical Jupyter Examples,” https://github.com/SFB-ELAINE/Biomedical-Jupyter-Examples

## Repository Structure

The repository is structured as follows:

1. `_Data` contains the raw data used for the analysis in the form of Excel sheets.
2. `EnhancedCalcium.bib` is used as central bibtex library used for references inside the Jupyter Notebooks.

For each programming language a separate folder is created that contains a single Jupyter Notebook document resembling the analysis as well as the corresponding PDF export.

For some programming languages additional files may be contained, e.g. for the documentation of package requirements.

## Usage

For each programming language a separate Docker image exists.
There are several methods of using the Jupyter Notebooks of this repository:

### Ready-to-use Docker Images

[![docker pulls](https://img.shields.io/docker/pulls/sfbelaine/biomedical-jupyter-notebooks.svg)](https://hub.docker.com/r/sfbelaine/biomedical-jupyter-notebooks/) [![docker stars](https://img.shields.io/docker/stars/sfbelaine/biomedical-jupyter-notebooks.svg)](https://hub.docker.com/r/sfbelaine/biomedical-jupyter-notebooks/) [![docker build](https://img.shields.io/docker/cloud/automated/sfbelaine/biomedical-jupyter-notebooks)](https://hub.docker.com/r/sfbelaine/biomedical-jupyter-notebooks/) [![docker build status](https://img.shields.io/docker/cloud/build/sfbelaine/biomedical-jupyter-notebooks)](https://hub.docker.com/r/sfbelaine/biomedical-jupyter-notebooks/)

The probably easiest way is to use the corresponding docker image: sfbelaine/biomedical-jupyter-notebooks:`<programming-language>` e.g. for running the Python example execute the following command in your terminal:

```bash
$ docker run --rm \
    --name=biomedical-jupyter-python \
    -p 127.0.0.1:8888:8888 \
    -v "$PWD":/home/jovyan/work \
    --user root \
    -e NB_UID=$(id -u) \
    -e NB_GID=$(id -g) \
    sfbelaine/biomedical-jupyter-notebooks:python
```
The parameters configure the following:

1. `--rm` removes the container automatically after exiting,
2. `--name=biomedical-jupyter-python` gives the container the name `biomedical-jupyter-python` instead of a generated one,
3. `-p 127.0.0.1:8888:8888` binds the container port `8888` (3. part) to the host ip address `127.0.0.1` and port `8888` (2. part),
4. `-v "$PWD":/home/jovyan/work` binds the current directory `$PWD` to the container directory `/home/jovyan/work`,
5. `--user root` is needed in order to set the UID and GID of the user running the Jupyter service inside the container,
6. `-e NB_UID=$(id -u)` and `-e NB_GID=$(id -g)` are used to set the user and group ID to the same as the user on the host in order to enable write access to the volume mounted by `-v`.

To search available docker images, use the corresponding Docker Hub repository: https://hub.docker.com/r/sfbelaine/biomedical-jupyter-notebooks

### Locally Building Docker Image

Despite downloading a ready-to-use Docker image, it can also be build on a local computer.
After downloading/cloning this repository, navigate into the folder (e.g. on *nix systems use the tool `cd`) of the desired programming language and call the docker build command:

```bash
$ cd Python
$ docker build -t biomedical-jupyter-python .
```

Afterwards, navigate into the root directory of the repository  and create a new container using this image might by e.g. using the following commands:

```bash
$ cd ../
$ docker run --rm \
    --name=biomedical-jupyter-python \
    -p 127.0.0.1:8888:8888 \
    -v "$PWD":/home/jovyan/work \
    --user root \
    -e NB_UID=$(id -u) \
    -e NB_GID=$(id -g) \
    biomedical-jupyter-python
```

For detailed information on the parameters consider the section on Ready-to-use Docker Images above.

### Installing Requirements Locally

Instead of using one of the provided containerization solutions, the software requirements might also be installed locally.
For this, consider the corresponding programming language for more details.
In many cases, a file documenting the requirements such as for the Python package manager `pip` the `requirements.txt` file is provided.
Also consider the `Dockerfile` for an example install procedure.

## Troubleshooting

In case the Notebook claims about missing data you probably have started the Jupyter software inside the directory of the programming language.
As the data is located inside the `_Data` folder in the root directory of the repository, the folder cannot be found then.
Restart the Jupyter software inside the root directory of the repository instead and locate to the programming language that shall be tested.
