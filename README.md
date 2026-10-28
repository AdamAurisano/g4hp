# G4HP

## Repository Structure

* **g4hp.cc**: The main code. This is the Geant4 thin-target simulation that stores the kinematics of particle production in inelastic interactions.

* **ana/**: The directory containing the analysis macros.

  * **CreateYields.C**: Calculates yields from G4HP ntuples. Currently configured for proton + C hadron production.

  * **CreateInvXS.C**: Calculates invariant cross sections from the CreateYields.C output.

  * **CreateMult.C**: Calculates multiplicities from G4HP ntuples. Currently configured for charged pion + C hadron production.

  * **functions.cxx**: A set of auxiliary functions used to calculate the average invariant cross sections, as well as xF and pT.

## Example Ntuples
Some example G4HP ntuples for p+C at 31, 60, and 120 GeV are publicly available here:

* **CERNBox G4HP p+C Ntuples**: https://cernbox.cern.ch/s/bHhuQFJv9SN4S37

## Building and Running the Code
g4hp builds in the conda environment initialized using janus-flux/env/environment.yml of the janus-flux repository.

From janus-flux root, create and activate the environment:
```text
conda env create -f env/environment.yml
conda activate janus-flux
```
From g4hp/:
```text
cmake -S . -B build
cmake --build build -j4
```
(Legacy build on CVMFS: source setup_g4hp_cvmfs.sh)

### Running an example
Once compiled, you can run an example simulation (from g4hp/)
```text
./build/g4hp -t C -p proton -e 119.065 -l FTFP_BERT -n 10000 -y
```
Note: -e is the kinetic energy; setting it to 119.065 gives p = 120 GeV/c. -y skips the confirmation prompt.

### Output
The file created is written to g4hp_root_files/ created in the directory you run the command from (here g4hp/g4hp_root_files/).
To write it elsewhere, use `-k <dir>` or set the environment variable G4HP_ROOTDIR.
```text
<particle>_<energy>_<target>_<physicslist>_<run>.root
```
(The example file would be: proton_119.065_C_FTFP_BERT_1.root)

