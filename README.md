# Scalable gradients enable Hamiltonian Monte Carlo sampling for phylodynamic inference under episodic birth-death-sampling models.
This repository contains the scripts and XML files required to reproduce the analyses performed in the "Scalable gradients enable Hamiltonian Monte Carlo sampling for phylodynamic inference under episodic birth-death-sampling models." paper by Shao et al.

## Installing BEAST/BEAGLE
These analyses require installation of the `hmc-clock` branch of BEAST and either the v4.0.0 release of BEAGLE or the `hmc-clock` branch of BEAGLE.

## Setting up BEAGLE
If opting not to use the [v4.0.0 release of BEAGLE](https://github.com/beagle-dev/beagle-lib/releases/tag/v4.0.0), please follow the [BEAGLE installation instructions](https://github.com/beagle-dev/beagle-lib), but be sure to get the `hmc-clock` branch.

For Mac users, the following commands will compile the CPU version of BEAGLE.
Follow the [instructions](https://github.com/beagle-dev/beagle-lib) if you need to install any other dependent software, ignore the first 2 lines if you already have all requisite dependencies installed.

```
xcode-select --install
brew install libtool autoconf automake
git clone https://github.com/beagle-dev/beagle-lib.git
cd beagle-lib
git checkout hmc-clock
mkdir build
cd build
cmake -DBUILD_CUDA=OFF -DBUILD_OPENCL=OFF ..
sudo make install
```


For Linux users, the commands are similar.

```
sudo apt-get install build-essential autoconf automake libtool git pkg-config openjdk-9-jdk
git clone https://github.com/beagle-dev/beagle-lib.git
cd beagle-lib
git checkout hmc-clock
mkdir build
cd build
cmake -DBUILD_CUDA=OFF -DBUILD_OPENCL=OFF ..
sudo make install
```

The libraries are installed into `/usr/local/lib`.

### Setting up BEAST

The following commands will compile the `hmc-clock` branch of BEAST.

```
git clone https://github.com/beast-dev/beast-mcmc.git
cd beast-mcmc
git checkout hmc-clock
ant
```

For Mac users, you may need to install ant using `brew install ant` via [Homebrew](https://brew.sh/).

For Linux users, you can install ant by `sudo apt-get install ant`.

This will compile the `jar` file `beast.jar` in `beast-mcmc/build/dist/beast.jar` which can be called to execute BEAST.

### Running BEAST with BEAGLE
To test that BEAST can use the BEAGLE implementation, one may run BEAST with the `-beagle_info` flag which will simply print all available computational resources to screen.
No XML need be supplied, e.g. `java -jar /path/to/beast-mcmc/build/dist/beast.jar -beagle_info`.

If BEAST cannot find BEAGLE, try the following:
- Call BEAST with the `-Djava.library.path` flag set to point to BEAGLE, e.g. `java -Djava.library.path=/path/to/where/beagle/is/installed -jar /path/to/beast-mcmc/build/dist/beast.jar -beagle_info`
- Add the location of BEAGLE to your PATH by running `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/usr/local/lib` before calling BEAST.

More information about installing BEAGLE is available in the [BEAGLE repository](https://github.com/beagle-dev/beagle-lib).

## Reproducing the analyses

You may use the following commands to run the analyses described in the manuscript.


From the top level of `hmc_ebds`, create and change directories to `output`.
```
mkdir output
cd output
```

As written, run commands will lead to the output files being placed in `hmc_ebds/output`.
If you wish them to be elsewhere, you may set the working directory to any directory where you want to store the resulting log files first, and amend the path to the xmls in the commands as needed.

Where ten replicate chains were run, the first seed is provided. The other seeds are 6662 to 66610.

### HIV dynamics in Odesa, Ukraine

The analyses on this dataset are:
- Fixed phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../HIV/HIV_fixed_HMC.xml
  ```
- Fixed phylogeny inference with MH-MCMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../HIV/HIV_fixed_MHMCMC.xml
  ```
- Joint phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../HIV/HIV_joint_HMC.xml
  ```
- Joint phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../HIV/HIV_joint_HMC.xml
  ```


### Seasonal Influenza in New York State

The analyses on this dataset are:
- Fixed phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Influenza/Influenza_fixed_HMC.xml
  ```
- Fixed phylogeny inference with MH-MCMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Influenza/Influenza_fixed_MHMCMC.xml
  ```
- Joint phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Influenza/Influenza_joint_HMC.xml
  ```
- Joint phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Influenza/Influenza_joint_HMC.xml
  ```



### Ebola epidemic in West Africa

The analyses on this dataset are:
- Fixed phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Ebola/ebol_fixed_HMC.xml
  ```
- Fixed phylogeny inference with MH-MCMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Ebola/ebol_fixed_MHMCMC.xml
  ```
- Joint phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Ebola/ebol_joint_HMC.xml
  ```

- Joint phylogeny inference with HMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Ebola/ebol_joint_MHMCMC.xml
  ```
