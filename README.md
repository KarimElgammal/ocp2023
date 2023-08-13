# OCP2023 challenge
Here comes our proposed solution to the OC23 challenge

- A good first step is to make adsorbML work with OCP darasets, for those details see [here](https://github.com/Open-Catalyst-Project/ocp/blob/main/INSTALL.md) to install OCP and the docker image details in [here](https://github.com/Open-Catalyst-Project/tutorial/blob/main/.devcontainer/Dockerfile) to install adsorbML with OCP.

- You can find excellent example scripts in the OCP team tutorial for adsorbML and OCP [here](https://github.com/Open-Catalyst-Project/tutorial/tree/main) 

- This tutorial notebooks is used here in this repo

<div style="background-color: #DFF0D8; color: #4F8A10; padding: 10px">
    <strong>Note:</strong> These scripts are inspired from https://github.com/Open-Catalyst-Project/tutorial/tree/main 
</div>
- You can use the docker file in the tutorial repo to build the docker image, by default it is CPU, maybe change to the yml GPU file to use GPU (it didn't work with me, probably the mamba docker image needs to be changed to one with nvidia drivers)

```bash
git clone https://github.com/Open-Catalyst-Project/tutorial.git
```
- Run the docker container

```bash
docker run -it --rm -p 8888:8888 -v "${PWD}":/home/mambauser/tutorial ocp-tutorial jupyter-lab --ip=0.0.0.0 --no-browser
```

or if you use vs-code you can use:

```bash
docker run -p 8888:8888 -v "${PWD}":/home/mambauser/tutorial --name ocp2023 ocp-tutorial
docker start ocp2023
```

## Here comes installation using conda and mamba
commands to install the packages for OCP:

```bash
 pyenv install miniconda3-latest
 pyenv local miniconda3-latest
 git clone https://github.com/Open-Catalyst-Project/ocp.git
 cd ocp
 conda install mamba -n base -c conda-forge
 conda install conda-merge -n base -c conda-forge
 conda install -n base -c defaults -c conda-forge python=3.9.* pip
 pip install conda-merge
 conda-merge env.common.yml env.gpu.yml > env.yml
 mamba env create -f env.yml
#activate the environment
 conda activate ocp-models
#install additional packages
 mamba install -n base -c conda-forge jupyterlab jupyter-book
 mamba clean --all
 pip install e3nn
 pip install ipykernel nbformat ipywidgets
 pip install -e .
 cd ..
 git clone https://github.com/Open-Catalyst-Project/Open-Catalyst-Dataset.git

```

To use the environment:

```bash
 pyenv local  miniconda3-latest
 conda activate ocp-models
```

To check if installation is working, use notebook [0_deal_with_checkpoints.ipynb](./0_deal_with_checkpoints.ipynb) here

<!-- 
#- To install the packages for OCP, we need conda and mamba first
#- I prefer to use pyenv, OCP team recommend conda with python 3.9 (miniconda3-3.9-4.12.0)
### Install pyenv
#```bash
#curl https://pyenv.run | bash
#```
#- Add the following to your .bashrc or .zshrc
#```bash
#export PATH="$HOME/.pyenv/bin:$PATH"
#eval "$(pyenv init -)"
#eval "$(pyenv virtualenv-init -)"
#```
#- Install miniconda3-3.9-4.12.0
#```bash
#pyenv install miniconda3-3.9-4.12.0
#```
#- Activate the miniconda version locally
#```bash
#pyenv local miniconda3-3.9-4.12.0
#```
#- Install mamba
#```bash
#conda install mamba -n base -c conda-forge
#```
#- Install conda-merge
#```bash
#conda install conda-merge -n base -c conda-forge
#```
#- install conda-forge and its pip
#```bash
#conda install -n base -c defaults -c conda-forge python=3.9.* pip
#```
#- install conda-forge with pip
#```bash
#pip install conda-merge
#```
#- clone the OCP repo
#```bash
#git clone https://github.com/Open-Catalyst-Project/ocp.git
#cd ocp
#```
#- use conda-merge to create the environment YAML file
#```bash
#conda-merge env.common.yml env.gpu.yml > env.yml
#```
#- Create the conda environment
#```bash
#conda env create -f env.yml
#```
-->