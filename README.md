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
To build the code, execute the following commands in your terminal:
```text
source setup_g4hp_cvmfs.sh
cmake .
make all
```
Running an example:
Once compiled, you can run an example simulation using:
```text
./g4hp -t C -p proton -e 120 -l FTFP_BERT -n 10000
```
