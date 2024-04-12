# Reconstructor - Current Version: 1.2.0
This repository contains all source code in the Reconstructor Python package, important file dependencies, and benchmarking scores for Reconstructor models. Reconstructor is a COBRApy compatible, automated GENRE building tool from annotated aminoa acid .fasta files based on KEGG annotations.

****Reconstructor is currently only compatible on MacOSX and Windows machines****
#### /RepresentativeGENRES
/RepresentativeGENRES/Reconstructor: Contains 10 representative bacterial GENRES in .sbml format created by Reconstructor from annotated .fasta files.

/RepresentativeGENREs/ModelSEED: Corresponding GENREs created with ModelSEED using the same genome sequence information as used in Reconstructor. 

/RepresentativeGRENREs/CarveME: Corresponding GENREs created with CarveME using genome sequences from the same species (or in one case, genus), but not exactly the same strain. These models were taken from the CarveME database ([https://github.com/cdanielmachado/carveme](https://github.com/cdanielmachado/carveme)).

#### /MEMOTE
Contains raw .html files for benchmarking scores for 10 representative Reconstructor models

See below in the __Supplementary Model Checks and Analyses__ at the bottom of the README for links to stable .html renderings of the MEMOTE scores and comparisons to other automatic model generation tools

#### /reconstructor
contains all package source code

# Installation Guide (Must have Python >= 3.8 installed):
## MacOSX

Install Reconstructor package using pip:
```
pip install reconstructor
```
Use following command to run Reconstructor's setup script and final installation checks (should take ~30min to complete depending on your system):
```
python -m reconstructor --test yes
```
## Windows

* Note: Windows users must install Reconstructor via Anaconda, as there are C dependencies not included in a standard Windows build environment

Install Reconstructor package using CMD.exe prompt launched from Anaconda navigator:
```
pip install reconstructor
```
Use following command to run Reconstructor's setup script and final installation checks (should take ~30min to run depending on your system):
```
python -m reconstructor --test yes
```

# Usage:
## Use reconstructor via COMMAND LINE

* You must run the setup script described in the Installation Guide before proceeding

Now that Reconstructor and all dependency databases are installed, you can proceed to use Reconstructor via command line. An example would be:
```
python -m reconstructor --input_file <input fasta file> --file_type <1,2,3> --gram <negative, positive> --media rich
```
#### Type 1: Build GENRE from annotated amino acid .fasta files
```
python -m reconstructor --input_file Osplanchnicus.aa.fasta --file_type 1 --gram negative --media rich
```

#### Type 2: Build GENRE from BLASTp hits
```
python -m reconstructor --input_file Osplanchnicus.hits.out --file_type 2 --gram negative --media rich
```

#### Type 3: Additional gap-filling (if necessary)
```
python -m reconstructor --input Osplanchnicus.sbml --type 3 --media rich
```
## Use Reconstructor directly in PYTHON
You can use Reconstructor directly in Python for using directly with COBRApy analysis tools.
To import the reconstruction function use the following line: 
``` 
from reconstructor import reconstruct
```
The reconstruct function is defined as follows, with the required argument being input_file. All other arguments have default options following the equals sign. Argument descriptions are provided below
```
reconstruct(input_file, file_type = 1, media=[], org = 'default', min_frac = 0.01, max_frac = 0.5, gram='none', out = 'default', name = 'default', cpu = 1, gapfill = 'yes')
```
Here is an example of how to generate a GENRE from an annotated amino acid fasta file (.fa, type 1 input) directly in your python script.
```
model = reconstruct('218496.4.fa', file_type = 1, gram = 'negative')
```
### Required and optional arguments
```
--input_file <REQUIRED input file, Required, str>
```
```
--file_type <REQUIRED input file type, .fasta = 1, diamond blastp output = 2, .sbml = 3, Required, Default = 1, int> 
```
```
--gram <REQUIRED Type of Gram classificiation (positive or negative), default = positive, str>
```
```
--media <REQUIRED 'rich' is the default and can be used to generate model based on a rich media. List of strings of metabolites in modelseed namespace composing the media condition, comma separated. Must end with _e. For example: 'cpd00001_e'.>
```
```
--org <KEGG organism code. Not required, str>
```
```
--min_frac <Minimum objective fraction required during gapfilling, default = 0.01, float>
```
```
--max_frac <Maximum objective fraction allowed during gapfilling, default = 0.5 ,float>
```
```
--out <Name of output GENRE file, default = default, str>
```
```
--name <ID of output GENRE, default = default, str>
```
```
--cpu <Number of processors to use, default = 1, int>
```

```
--test <run installation tests, default = no, str>
```

# Supplementary Model Checks and Analyses

## MEMOTE Comparison of Reconstructor, ModelSEED, and CarveME GENREs
To view rendered .html MEMOTE benchmarking scores for Reconstructor models and the corresponding ModelSEED/CarveME models, use the links below:  
__*Porphyromonas gingivalis:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/837.134.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/837.83MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/837.83C.html)  
__*Bacillus amyloliquefaciens:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/1390.556.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/1390.556MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/1390.556C.html)  
__*Citrobacter braakii:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/57706.84.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/57706.84MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/57706.84C.html)  
__*Acinetobacter bereziniae:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/106648.24.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/106648.24MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/106648.24C.html)  
__*Tropheryma whipplei:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/218496.4.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/218496.4MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/218496.4C.html)  
__*Proteus mirabilis:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/529507.6.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/529507.6MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/529507.6C.html)  
__*Clostridiodes difficile:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5C.html)  
__*Campylobacter jejuni:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/1349827.3.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/1349827.3MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/1349827.3C.html)  
__*Helicobacter pylori:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/1382925.3.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/1382925.3MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/1382925.3C.html)  
__*Escherichia coli:*__ [Resonstructor](https://emmamglass.github.io/ReconstructorMEMOTE.io/2848143.3.redo.html) || [ModelSEED](https://emmamglass.github.io/ReconstructorMEMOTE.io/2848143.3MS.html) || [CarveME](https://emmamglass.github.io/ReconstructorMEMOTE.io/2848143.3C.html)

## *C. difficile* reconstructions on Complete (Default), Rich, Minimal, *C. difficile* Defined Minimal, *C. difficile* Defined Enriched

#### /C_difficile_Media
This folder contains .sbml reconstrucitons for *C. difficile* on five different media conditions described below. These include a complete media (default reconstructor media if no media is defined), rich media (built into reconstructor), minimal media (built into reconstructor), *C. difficile* specific defined minimal media (user inputted), and a *C. difficile* specific defined enriched media (user inputted). 

__Default media__ contains the following ModelSEED compounds:  
cpd00035 (L-Alanine), cpd00051 (L-Arginine), cpd00132 (L-Asparagine), cpd00041 (L-Aspartate), cpd00084 (L-Cysteine), cpd00053 (L-Glutamine), cpd00023 (L-Glutamate), cpd00033 (Glycine), cpd00119 (L-Histidine), cpd00322 (L-Isoleucine), cpd00107 (L-Leucine), cpd00039 (L-Lysine), cpd00060 (L-Methionine), cpd00066 (L-Phenylalanine), cpd00129 (L-Proline), cpd00054 (L-Serine), cpd00161 (L-Threonine), cpd00065 (L-Tryptophan), cpd00069 (L-Tyrosine), cpd00156 (L-Valine), cpd00027 (D-Glucose), cpd00149 (Cobalt), cpd00030 (Manganese), cpd00254 (Magnesium), cpd00971 (Sodium), cpd00063 (Calcium), cpd10515 (Iron), cpd00205 (Potassium), cpd00099 (Choride)  
This reconstruction was generated using the following arugments:  
```
--input 699034.5.fa --type 1 --gram positive  
```
The MEMOTE scores for *C. difficile* reconstruction in complete media can be found [here](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5.redo.html)  

__Rich media__ contains the following ModelSEED compounds:  
cpd00001 (Water), cpd00035 (L-Alanine), cpd00041(L-Aspartate), cpd00023 (L-Glutamate), cpd00119 (L-Histidine), cpd00107 (L-Leucine), cpd00060 (L-Methionine), cpd00161 (L-Threonine), cpd00069 (L-Tyrosine), cpd00084 (L-Cysteine), cpd00033 (Glycine), cpd00322 (L-Isoleucine acid), cpd00066 (L-Phenylalanine), cpd00054 (L-Serine), cpd00065 (L-Tryptophan), cpd00156 (L-Valine), cpd00220 (Riboflavin), cpd00644 (Pantothenate), cpd00393 (Folate), cpd00133 (Nicotinamide), cpd00263 (Pyridoxal), cpd00104 (Biotin), cpd00149 (Cobalt), cpd00971 (Sodium), cpd00099 (Chloride), cpd00205 (Potassium), cpd00009 (Phosphate), cpd00063 (Calcium), cpd00254 (Magnesium), cpd10515 (Iron), cpd00030 (Manganese), cpd00242 (Bicarbonate), cpd00226 (Hypoxanthine), cpd01242 (Thyminose), cpd00307 (Cytosine), cpd00092 (Uracil), cpd00117 (D-Alanine), cpd00067 (Hydrogen), cpd00567 (D-Proline), cpd00132 (L-Asparagine), cpd00210 (Taurine), cpd00320 (D-Aspartate), cpd03279 (Deoxyinosine) , cpd00246 (Inosine), cpd00311 (Guanosine), cpd00367 (Cytidine), cpd00277 (Deoxyguanosine), cpd00182 (Adenosine), cpd00654 (Deoxycytidine), cpd00412 (Deoxyuridine), cpd00438 (Deoxyadenosine), cpd00274 (Citrulline), cpd00186 (D-Glutamate), cpd00637 (D-Methionine), cpd00105 (D-Ribose), cpd00305 (Thiamin), cpd00309 (Xanthine), cpd00098 (Choline), cpd00207 (Guanine), cpd00082 (D-Fructose), cpd00129 (L-Proline)
This reconstruction was generated using the following arugments:  
```
--input 699034.5.fa --type 1 --gram positive --media rich_media  
```
The MEMOTE scores for *C. difficile* reconstruction in rich media can be found [here](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5.richmedia.html)  

__Minimal media__ contains the following ModelSEED compounds:  
cpd00001 (Water), cpd00065 (L-Tryptophan), cpd00060 (Methionine), cpd00322 (L-Isoleucine), cpd00129 (L-Proline), cpd00156 (L-Valine), cpd00107 (L-Leucine), cpd00084 (L-Cysteine), cpd00149 (Cobalt), cpd00099 (Chloride), cpd10515 (Iron), cpd00030 (Manganese), cpd00254 (Magnesium), cpd00063 (Calcium), cpd00205 (Potassium), cpd00009 (Phosphate), cpd00971 (Sodium), cpd00242 (Carbonate), cpd00104 (Biotin), cpd00644 (Pantothenate), cpd00263 (Pyridoxine) , cpd00082 (D-Fructose) 
This reconstruction was generated using the following arugments:  
```
--input 699034.5.fa --type 1 --gram positive --media minimal_media  
```
The MEMOTE scores for *C. difficile* reconstruction in minimal media can be found [here](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5.minimalmedia.html) 

__*C. difficile* defined minimal media__ contains the following ModelSEED compounds:  
cpd00001 (Water), cpd00104 (Biotin), cpd00644 (Pantothenate), cpd00263 (Pyridoxine), cpd00149 (Cobalt), cpd00099 (Chloride), cpd10515 (Iron), cpd00030 (Manganese), cpd00254 (Magnesium), cpd00063 (Calcium), cpd00205 (Potassium), cpd00009 (Phosphate), cpd00971 (Sodium), cpd00242 (Carbonate), cpd00322 (L-Isoleucine), cpd00129 (L-Proline),  cpd00156 (L-Valine), cpd00107 (L-Leucine), cpd00084 (L-Cysteine), cpd00065 (L-Tryptophan), cpd00027 (Glucose)  
This reconstruction was generated using the following arguments:  
```
--input 699034.5.fa --type 1 --gram positive --media 'cpd00001_e','cpd00104_e','cpd00644_e','cpd00263_e','cpd00149_e','cpd00099_e','cpd10515_e','cpd00030_e','cpd00254_e','cpd00063_e','cpd00205_e','cpd00009_e','cpd00971_e','cpd00242_e','cpd00322_e','cpd00129_e','cpd00156_e','cpd00107_e','cpd00084_e','cpd00065_e','cpd00027_e'
```
The MEMOTE scores for *C. difficile* reconstruction in minimal defined media can be found [here](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5.definedminimal.html) 

__*C. difficile* defined enriched media__ contains the following ModelSEED compounds:  
cpd00035 (Alanine), cpd00041 (Aspartic Acid), cpd00023 (Glutamic Acid), cpd00119 (Histidine), cpd00107 (Leucine), cpd00060 (Methionine), cpd00129 (Proline), cpd00161 (Threonine), cpd00051 (Arginine), cpd00069 (Tyrosine), cpd00084 (Cysteine), cpd00033 (Glycine), cpd00322 (Isoleucine), cpd00039 (Lysine), cpd00066 (Phenylalanine), cpd00054 (Serine), cpd00065 (Tryptophan), cpd00156 (Valine), cpd00027 (Glucose),
cpd00220 (Riboflavin), cpd00644 (Calcium Pantothentate), cpd00393 (Folate), cpd00133 (Niacin), cpd00263 (Pyridoxine), cpd00104 (Biotin), cpd00149 (Cobalt), cpd00971 (Sodium), cpd00099 (Chloride), cpd00205 (Potassium), cpd00009 (Phosphate), cpd00063 (Calcium),
cpd00254 (Magnesium), cpd10515 (Fe2+), cpd00030 (Mn2+), cpd00242 (Carbonate), cpd00001 (Water), cpd00226 (Hypoxanthine), cpd01242 (Thyminose), cpd00307 (Cytosine), cpd00092 (Uracil)  
This reconstruction was generated using the following arguments" 
```
--input 699034.5.fa --type 1 --gram positive --media 'cpd00035_e','cpd00041_e','cpd00023_e','cpd00119_e','cpd00107_e','cpd00060_e','cpd00129_e','cpd00161_e','cpd00051_e','cpd00069_e','cpd00084_e','cpd00033_e','cpd00322_e','cpd00039_e','cpd00066_e','cpd00054_e','cpd00065_e','cpd00156_e','cpd00027_e','cpd00220_e','cpd00644_e','cpd00393_e','cpd00133_e','cpd00263_e','cpd00104_e','cpd00149_e','cpd00971_e','cpd00099_e','cpd00205_e','cpd00009_e','cpd00063_e','cpd00254_e','cpd10515_e','cpd00030_e','cpd00242_e','cpd00001_e','cpd00226_e','cpd01242_e','cpd00307_e','cpd00092_e'
```
The MEMOTE scores for *C. difficile* reconstruction in enriched defined media can be found [here](https://emmamglass.github.io/ReconstructorMEMOTE.io/699034.5.definedrich.html) 

# User-Specified Universal Database Modification
The universal reaction database used in reconstructor is a modified version of the ModelSEED biochemistry database avaliable [here](https://github.com/ModelSEED/ModelSEEDDatabase). We generated the universal database using the __UniversalCreation.py__ script. We corrected poorly defined metabolite formulas and removed mass imbalanced reactions using the __curateuniversal.py__ script that is avaliable in this repository.  

If you wish to modify the provided universal reaction database you must first locate the universal.pickle file that was downloaded during the reconstructor installation phase on your local computer. You can modify this file by running a python script. You must write this script yourself or use __curateuniversal.py__ as a template. You can then run this script in your command line. 

### Dependencies and loading universal.pickle
Begin your script with the following dependencies:
```
import os
import cobra
import pickle
import argparse
import warnings
import symengine
from random import shuffle
from multiprocessing import cpu_count
from sys import stdout
from copy import deepcopy
from subprocess import call
from cobra.util import solver
from cobra.manipulation.delete import *
```
Then, load your universal.pickle file using:  
```
filename = '/universal.pickle'
with open(filename, 'rb') as f: universal = pickle.load(f)
```
Now you can freely add, change, or remove reactions and metabolites from the universal reaction database. You can add, remove, or modify reactions and metabolites from the universal database in the same way you would add, remove, or modify reactions and metabolites in a GENRE. Some examples of how to do this are below, but you can see further examples in the [cobrapy documentation](https://cobrapy.readthedocs.io/en/latest/building_model.html).  

### Modifying existing metabolites
If you want to change the formula, of a specific metabolite formula you can do so like below
```
universal.metabolites.cpd17677_e.formula = 'C17H24O2'
```

```
universal.metabolites.cpd17677_e.name = 'new_name'
```
### Adding reactions
You can add reactions to the universal database by defining the reaction, and then adding it to the model.
```
universal.reaction.add_metabolites({
    malACP_c: -1.0,
    h_c: -1.0,
    ddcaACP_c: -1.0,
    co2_c: 1.0,
    ACP_c: 1.0,
    omrsACP_c: 1.0
})
```
```
universal.add_reactions([reaction])
```

### Removing reactions and metabolites
Examples of removing metabolites and reactions from the universal database are shown below.  
For a reaction named rxn:
```
universal.remove_reactions(rxn)
```

For a metabolite named met:
```
universal.remove_metabolites(met)
```
### Saving new universal database
After making modifications to the universal database, you can replace the existing universal database using the following command or similar:
```
pickle.dump(universal, open(script_path + '/universal.pickle', 'wb'))
```

# Additional Information
Thank you for your interest in Reconstructor. If you have any additional questions please email tfz5vy@virginia.edu.

If you encounter any problems, please file an [issue](https://github.com/emmamglass/reconstructor/issues) along with a detailed description.

Distributed under the terms of the [MIT license](https://github.com/emmamglass/reconstructor/blob/main/reconstructor/LICENSE), "reconstructor" is free and open source software
