# Gromacs WSL2
Install Gromacs on WSL2 in simple steps

##There are two methosa for this
1. [Method 1: Source Code Building & Installation of Gromacs](#method-1-source-code-building--installation-of-gromacs) (Hard process & technical knowledge needed)
2. [Method 2: DEB Package Installation of Gromacs](#method-2-deb-package-installation-of-gromacs) (Easy process & no technical knowledge needed)

# Method 1: Source Code Building & Installation of Gromacs
## Setting up the environment
```
sudo apt update && upgrade -y
sudo apt install libfftw3-mpi-dev python3-full python3-pip pipx -y
sudo apt install build-essential doxygen  -y 
sudo apt-get install openmpi-bin openmpi-doc libopenmpi-dev -y
pipx install sphinx --include-deps
pipx install gmxvg --include-deps
```
## Downloading Gromacs 2024.2
```
mkdir gromacs && cd gromacs
wget -O gromacs.tar.gz https://ftp.gromacs.org/gromacs/gromacs-2024.2.tar.gz
tar xvfz gromacs.tar.gz
cd gromacs-2024.2
```
## Creating build directory
```
mkdir build && cd build
```
## Building Gromacs
  - FOR GPU SYSTEMS
  ```
  cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=ON -DGMX_GPU=CUDA
  make -j$(nproc)
  ```
  - FOR CPU SYSTEMS
  ```
  cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=ON -DGMX_GPU=OFF
  make -j$(nproc)
  ```
## Check build (Optional => Takes more than 4 hours, atleast on my system)
```
make check
```
## Install Gromacs
```
sudo make install
```
## Edit file '~/.bashrc'
```
nano ~/.bashrc
```
## Add these 2 lines into ~/.bashrc:
```
export PATH=/usr/local/gromacs/bin${PATH:+:${PATH}}
export PATH=/usr/local/gromacs/bin/GMXRC${PATH:+:${PATH}}
```
## Save file
`ctrl+x => exit`<br>
`y => saves file name`<br>
`{enter-key} => saves file`
## Execute '~/.bashrc' to save paths
```
source ~/.bashrc
```
## Remove downloaded files to save space
```
sudo cd ../../ && rm -rf gromacs*
```
## Check Gromacs installation and version
```
gmx -V
```
[Installed Successfully, the latest version available (2024.2)]

# Method 2: DEB Package Installation of Gromacs

## Setting up the environment
```
sudo apt update && upgrade -y
sudo apt install libfftw3-mpi-dev python3-full python3-pip pipx -y
sudo apt install build-essential doxygen  -y
sudo apt install glibc-source -y
sudo apt-get install openmpi-bin openmpi-doc libopenmpi-dev -y
pipx install sphinx --include-deps
pipx install gmxvg --include-deps
```
## Download &  Install precompiled DEB Package
  - FOR GPU SYSTEMS
  ```
  mkdir gromacs && cd gromacs
  wget<link>
  dpkg -i <file>
  ```
  - FOR CPU SYSTEMS
  ```
  mkdir gromacs && cd gromacs
  wget<link>
  dpkg -i <file>
  ```
## Remove downloaded files to save space
```
sudo cd ../../ && rm -rf gromacs*
```
## Check Gromacs installation and version
```
gmx -V
```
[Installed Successfully, the latest version available (2024.2)]
