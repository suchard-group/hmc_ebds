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

### RevBayes

Reproducing the RevBayes analysis requires the installation of the `bdss-timing` branch of [RevBayes](https://www.beast2.org/tutorials/). Compiling instructions can be found in the [tutorial](https://revbayes.github.io/compile-osx) on RevBayes website.

Then we can set the working directory to `hmc_ebds/Benchmark/`
and use RevBayes to run the example Rev scripts in the relevant `/RevBayes` subdirectory.

- The `Epoch_benchmark.Rev` is the script for analyses of the likelihood calculation time for an increasing number of epochs.
- The `rev_benchmarking_script_template.Rev` is a template that user can modify to reproduce all the experiments in this study.

### TreePar

The required TreePar package can be downloaded from [CRAN](https://cran-archive.r-project.org/web/checks/2022/2022-04-27_check_results_TreePar.html) archive. The R script for running the timing experiment for an increasing number of epochs is provided in the directory `hmc_ebds/Benchmark/TreePar`. To reproduce results from analysis with an increasing number of sequences, we can simply change the directory to the desired tree file under `hmc_ebds/Benchmark/simulated_trees` and the corresponding nodes in the R script.

### VBSKY

We first download the modified copy of the VBSKY package under `gradient-timing` branch for [VBSKY](https://github.com/yucais/vbcompare/tree/gradient-timing). Then using the graphical user interface of your computer, enter the `vbcompare` folder. Then use the following commands to run the analysis.

  ```
  conda activate vbsky
  cd example
  bash bash run_exp.sh
  ```

Note that one can change the values of `ntips(t)` and `epochs(i)` in `run_exp.sh` to reproduce all the timing experiment results in this study.
