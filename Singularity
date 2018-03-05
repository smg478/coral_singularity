Bootstrap: docker
From: nvidia/cuda:9.1-cudnn7-devel-ubuntu16.04

# adapted from: https://github.com/marcc-hpc/anaconda-cuda

%environment

  # use bash as default shell
  SHELL=/bin/bash

  # add CUDA paths
  CPATH="/usr/local/cuda/include:$CPATH"
  PATH="/usr/local/cuda/bin:$PATH"
  LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
  CUDA_HOME="/usr/local/cuda"

  # add Anaconda path
  PATH="/usr/local/anaconda3/bin:$PATH"

  export PATH LD_LIBRARY_PATH CPATH CUDA_HOME

%setup
  # runs on host
  # the path to the image is $SINGULARITY_ROOTFS

%post
  # post-setup script

  # load environment variables
  . /environment

  # use bash as default shell
  echo "\n #Using bash as default shell \n" >> /environment
  echo 'SHELL=/bin/bash' >> /environment

  # make environment file executable
  chmod +x /environment

  # default mount paths
  mkdir /scratch

  #Add CUDA paths
  echo "\n #Cuda paths \n" >> /environment
  echo 'export CPATH="/usr/local/cuda/include:$CPATH"' >> /environment
  echo 'export PATH="/usr/local/cuda/bin:$PATH"' >> /environment
  echo 'export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"' >> /environment
  echo 'export CUDA_HOME="/usr/local/cuda"' >> /environment

  # updating and getting required packages
  apt-get update && apt-get -y install locales
  locale-gen en_US.UTF-8
  apt-get install -y wget git vim build-essential cmake

  # creates a build directory
  mkdir build
  cd build

  # download and install Anaconda
  CONDA_INSTALL_PATH="/usr/local/anaconda3"
  wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
  chmod +x Anaconda3-5.0.1-Linux-x86_64.sh
  ./Anaconda3-5.0.1-Linux-x86_64.sh -b -p $CONDA_INSTALL_PATH

  # make and install conda environment
  

%runscript
  # executes with the singularity run command
  # delete this section to use existing docker ENTRYPOINT command

%test
  # test that script is a success