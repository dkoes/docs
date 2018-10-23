# Linux Setup

These instructions may apply equally well to the [Linux Subsystem for Windows](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

For Mac, you should use [MacPorts](https://www.macports.org/) for installing packages.

## Install prerequisites 

Some common packages.

`apt-get install build-essential git wget libopenbabel-dev libboost-all-dev libeigen3-dev libgoogle-glog-dev libprotobuf-dev protobuf-compiler libhdf5-serial-dev libatlas-base-dev python-dev cmake librdkit-dev python-pip imagemagick`

Some common python packages:

`sudo pip install matplotlib scipy sklearn scikit-image protobuf psutil numpy seaborn jupyter plumbum MDAnalysis biopython Pillow prody py3dmol pandas cython`


## Environment

In your `.bashrc` configure the history:
```
HISTCONTROL=ignoredups
export PROMPT_COMMAND="history -a"
shopt -s histappend
export HISTSIZE=1000000
```
