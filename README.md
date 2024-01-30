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
- Joint phylogeny inference with MH-MCMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../HIV/HIV_joint_MHMCMC.xml
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
- Joint phylogeny inference with MH-MCMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Influenza/Influenza_joint_MHMCMC.xml
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

- Joint phylogeny inference with MH-MCMC
  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Ebola/ebol_joint_MHMCMC.xml
  ```
## Timing Experiments
### BEAST
To enable benchmark analyses for likelihood and gradient calculations, we need to change the Boolean value `MEASURE_RUN_TIME` to `true` in java two classes `.../beast-mcmc/src/dr/evomodel/speciation/EfficientSpeciationLikelihood.java` and `.../beast-mcmc/src/dr/evomodel/speciation/CachedGradientDelegate.java`. Then we can build the BEAST program by compile the `jar` file `beast.jar` in `beast-mcmc/build/dist/beast.jar`.
Similarly, we can use BEAST to run the XML files provided in the directory `hmc_ebds/Benchmark/beast`. 

  - The folder `epoch` contains XML files for reproducing results for likelihood timing experiments with an increasing number of epochs. File names correspond to the number of epochs used in this analysis.
  - The folder `seq` contains XML files for reproducing results for likelihood timing experiments with an increasing number of sequences. File names correspond to the number of sequences used in this analysis.
  - The folder `gradient_epoch` contains XML files for reproducing results for gradient timing experiments with an increasing number of epochs. File names correspond to the number of epochs used in this analysis.
  - The folder `gradient_seq` contains XML files for reproducing results for gradient timing experiments with an increasing number of sequences. File names correspond to the number of sequences used in this analysis.

We can use the same commands as the previous section to run the analysis, which is demonstrated below:

  ```
  java -Djava.library.path=/usr/local/lib \
  -jar /path/to/beast-mcmc/build/dist/beast.jar \
  -seed 6661 -overwrite \
  ../Benchmark/beast/epoch/5.xml
  ```

Simply changing the XML file name in the directory in the above command allows us to run all XML files in the provided folder.

### BEAST2
Running the analysis requires [BEAST2](https://www.beast2.org/) version 2.6.0 or higher and the modified BEAST2 package [BDSKY](https://github.com/yucais/bdsky_benchmark). We can use BEAST2 to run the XML files provided in the directory `hmc_ebds/Benchmark/beast2`

  - The folder `epoch` contains XML files for reproducing results for likelihood timing experiments with an increasing number of epochs. File names correspond to the number of epochs used in this analysis. 
  - The folder `seq` contains XML files for reproducing results for likelihood timing experiments with an increasing number of sequences. File names correspond to the number of sequences used in this analysis.

Instructions on how to set up BEAST2, load the required package and run an XML file can be found in the [tutorial](https://www.beast2.org/tutorials/) on BEAST2 website.

### Revbayes

Reproducing the Revbayes analysis requires the installation of the `bdss-timing` branch of [Revbayes](https://www.beast2.org/tutorials/). Compiling instructions can be found in the [tutorial](https://revbayes.github.io/compile-osx) on Revbayes website.

Then we can set the working directory to `hmc_ebds/Benchmark/`
and use RevBayes to run the example Rev scripts in the relevant `/Revbayes` subdirectory.

- The `Epoch_benchmark.Rev` is the script for analyses of the likelihood calculation time for an increasing number of epochs.
- The `rev_benchmarking_script_template.Rev` is a template that user can modify to reproduce all the experiments in this study.

### TreePar

The required TreePar package can be downloaded from [CRAN](https://cran-archive.r-project.org/web/checks/2022/2022-04-27_check_results_TreePar.html) archive. The R script for running the timing experiment for an increasing number of epochs is provided in the directory `hmc_ebds/Benchmark/TreePar`. To reproduce results from analysis with an increasing number of sequences, we can simply change the directory to the desired tree file under `hmc_ebds/Benchmark/simulated_trees` and the corresponding nodes in the R script.

### VBSKY

We first download the modified copy of the VBSKY package under `modified_ver` branch for [VBSKY](https://github.com/yucais/vbcompare/tree/modified_ver). Then using the graphical user interface of your computer, enter the `vbcompare` folder. Then use the following commands to run the analysis.

  ```
  conda activate vbsky
  cd example
  bash bash run_exp.sh
  ```

Note that one can change the values of `ntips(t)` and `epochs(i)` in `run_exp.sh` to reproduce all the timing experiment results in this study,
