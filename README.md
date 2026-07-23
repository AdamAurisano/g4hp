* Building the code
- source setup_g4hp_cvmfs.sh
- cmake .
- make all
and run man example: ./g4hp -t C -p proton -e 120 -l FTFP_BERT -n 10000

* Structure:
- Main code is include and src contain the Geant4 thin target simulation storing the kinematics of particle production in inelastic interactions.
- An analyusis directory ana
make
CreateYields.C : makes yields from G4HP ntuples. Currently set for proton + C hadron production
CreateInvXS.C : makes invariant cross sections from the CreateYields.C output.
CreateMult.C. : makes multiplicities from G4HP ntuples. Currently set for charged pion + C hadron production
functions.cxx : is a set of functions to calculate the average invariant cross sections as well as xF and pT.
We make a library with these functions. An example to run is in ExampleOfUsingFunctions.C
(run it with ./ExampleOfUsingFunctions)
