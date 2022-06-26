# **NUCLEAR configuration file parameters**

NUCLEAR uses a configuration file to specify all their required parameters. Users must decide what job to perform; **(i)** a molecular hotspot determination or **(ii)** an oligonucleotide search. For a hotspot determination, the sections *\[inputs\]*, *\[mcss_files\]*, and *\[spots_params\]* are the only ones that should appear in the configuration file. If an oligonucleotide search is requested, then the mandatory sections are *\[inputs\]*, *\[mcss_files\]*, *\[zones_params\]*, *\[search_params\]*, and *\[minimization\]*. Below, all section parameters have been described.

## **Section \[inputs\]**

- **input_dir** &lt; path to the directory containing MCSS explorations &gt;  
 ***Acceptable Values:*** valid path.  
 ***Recommended Value:*** None  
 ***Description:*** Specifies the path to find the *.crd* files of MCSS docking results. NUCLEAR will check if this path exists.  
  
- **output_dir** &lt; path to the output directory &gt;  
 ***Acceptable Values:*** valid path.  
 ***Recommended Value:*** None  
 ***Description:*** Specifies the root path where NUCLEAR writes results. NUCLEAR will check if this path exists, in which case the program will stop to avoid overwriting previous results.  
  

- **prot_coords** < path to the *receptor.pdb* >  
 ***Acceptable Values:*** valid path  
 ***Recommended Value:*** None  
 ***Description:*** Specifies the path to the receptor *.pdb* coordinate file. NUCLEAR will check if this path exists and that the receptor file format is *.pdb*.  
  
- **ncores** &lt; number of cores for parallelization &gt;  
 ***Acceptable Values:*** integer >= 1  
 ***Recommended Value:*** 1  
 ***Description:*** Specifies the number of cores used to construct the matrix of clashes.  
  
## **Section \[mcss_files\]**   
  
\[mcss_files\] is a mandatory section that contains no parameter. Instead, users must specify one or more tuples of three blank-separated columns. Note that one of the two last columns (or both) must be N (unrestricted) to avoid selection ambiguities.  
  
**1st column (string):** The name of the *.crd* file (including the extension but not the path, already specified in the input_dir parameter).  
  
**2nd column (float):** Maximum score to be considered in the corresponding MCSS distribution. Poses having a higher score will not be considered.  
  
**3rd column (integer):** Number of poses to be considered in the corresponding MCSS distribution.  
  
## **Section \[spots_params\]**  
  
- **prot_sel** &lt; NUCLEAR protein selection &gt;  
 ***Acceptable Values:*** \[ all | heavy | protein \]  
 ***Recommended Value:*** protein  
 ***Description:*** Selection of protein atoms considered when calculating protein-ligand contact zone. Options are limited to all: all atoms in the *protein.pdb* file, heavy: non-hydrogen atoms in the *protein.pdb* file, and protein: protein atoms in the *protein.pdb* file.  
  
- **frag_sel** &lt; NUCLEAR fragment (ligand) selection &gt;  
 ***Acceptable Values:*** \[ all | all\_nopatch | heavy | heavy\_nopatch \]  
 ***Recommended Value:*** all_nopatch  
 ***Description:*** Selection of ligand atoms considered when calculating protein-ligand contact zone. Options are limited to all: all atoms in the *ligand.crd* file, all_nopatch: all atoms except patch ones in the *ligand.crd* file, heavy: non-hydrogen atoms in the *ligand.crd* file, and heavy_nopatch: non-hydrogen atoms except patch ones in the *ligand.crd* file. Patch atoms (not used when constructing oligonucleotides) are defined as: *\['C5T', 'O5T', 'O1P', 'O2P', 'H5T1', 'H5T2', 'H5T3'\]*  
  
- **inter_dist** &lt; Inter-atomic distance for contact zones calculation &gt;  
 ***Acceptable Values:*** float > 0.0  
 ***Recommended Value:*** 3.5  
 ***Description:*** Inter-atomic distance under which a contact between a ligand atom and a protein atom is declared  
  
- **density_cut** &lt; In hotspots detection, clusters having a density value under this cutoff get filtered out &gt;  
 ***Acceptable Values:*** 0.0 < float < 1.0  
 ***Recommended Value:*** 0.05  
 ***Description:*** Clusters having a density value under this cutoff get filtered out. The density of a cluster is calculated as the Number of poses it contains divided by the Number of distinct residues involved in the poses' contact zones. This magnitude is then normalized to the 0-1 interval.   
  
- **merge_cut** &lt; In hotspot detection, cluster seeds having a similarity value under this cutoff provokes their clusters to merge &gt;  
 ***Acceptable Values:*** 0.0 < float < 1.0  
 ***Recommended Value:*** 0.25  
 ***Description:*** In hotspot detection, cluster seeds having a similarity value under this cutoff provokes their clusters to merge. The similarity metric employed is the Tanimoto index (lowest values correspond to more similar seeds).  
  
## **Section \[zones_params\]**  
  
- **prot_sel** < idem to what is described in section **\[spots_params\]** >  
- **frag_sel** < idem to what is described in section **\[spots_params\]** >  
- **inter_dist** < idem to what is described in section **\[spots_params\]** >  
  
## **Section \[search_params\]**  
  
- **top_N** &lt; Number of top-N best-scored sequences to be returned &gt;  
 ***Acceptable Values:*** integer >= 1  
 ***Recommended Value:*** 500  
 ***Description:*** Number of top-N best-scored sequences to be returned. The sequence score is calculated as the summation of the scores of each composing nucleotide.  
  
- **seq\_min\_size** &lt; Minimum number of nucleotides in returned sequences &gt;  
 ***Acceptable Values:*** integer >= 2  
 ***Recommended Value:*** 2  
 ***Description:*** Minimum number of nucleotides in returned sequences. When seq\_to\_search is not all, this value must equal the number of nucleotides specified in the seq\_to\_search parameter.  
  
- **seq\_max\_size** &lt; Maximum number of nucleotides in returned sequences &gt;  
 ***Acceptable Values:*** integer >= seq\_min\_size  
 ***Recommended Value:*** N  
 ***Description:*** Maximum number of nucleotides in returned sequences. Users can retrieve the maximum number of nucleotides in returned sequences by setting this to N. When seq\_to\_search is not all, this value must equal the number of nucleotides specified in the seq\_to\_search parameter.  
  
- **seq\_to\_search** &lt; Sequence of nucleotides to search &gt;  
 ***Acceptable Values:*** \[ all | :-separated string of resnames \]  
 ***Recommended Value:*** all  
 ***Description:*** Sequence of nucleotides to search. The oligonucleotide sequence must comprise colon-separated strings corresponding to each nucleotide resname, as found in the corresponding crd files. The underscore _ can specify any nucleotide. When seq\_to\_search is not all, parameters seq\_max\_size must equal seq\_min\_size, and both must be set to the Number of nucleotides specified in seq\_to\_search.  
  
- **path\_to\_search** &lt; Atomic selection of protein residues to search &gt;  
 ***Acceptable Values:*** valid string selection (defined in agreement with ProDy syntax)  
 ***Recommended Value:*** \[all | valid string selection \]  
 ***Description:*** Atomic selection of protein residues. Only contact zones containing these residues indices will be considered.  
  
- **max\_dist\_O3C5** &lt; The maximum distance between O3' and C5' atoms may link consecutive nucleotides. &gt;  
 ***Acceptable Values:*** float > 0.0  
 ***Recommended Value:*** 4.0 A  
 ***Description:*** The maximum distance between O3' and C5' atoms may link consecutive nucleotides.  
  
- **clash_dist** &lt; Minimum distance to declare an atomic clash &gt;  
 ***Acceptable Values:*** 0.0 < float < max\_dist\_O3C5  
 ***Recommended Value:*** 2.0 A  
 ***Description:*** Minimum distance to declare an atomic clash. When atoms of different nucleotides inside an under-construction sequence are closer than this distance, a clash is declared, and the nucleotide provoking the clash is removed from the sequence.  
  
## **Section \[minimization\]**  
  
We will complete this section soon.  
  
self.prot\_topol = self.cfg\['minimization'\]\['prot\_topol'\]  
self.prot\_param = self.cfg\['minimization'\]\['prot\_param'\]  
self.na\_topol = self.cfg\['minimization'\]\['na\_topol'\]  
self.na\_param = self.cfg\['minimization'\]\['na\_param'\]  
self.carb\_topol = self.cfg\['minimization'\]\['carb\_topol'\]  
self.carb\_param = self.cfg\['minimization'\]\['carb\_param'\]  
self.cgenff\_topol = self.cfg\['minimization'\]\['cgenff\_topol'\]  
self.cgenff\_param = self.cfg\['minimization'\]\['cgenff\_param'\]  
self.namod\_toppar = self.cfg\['minimization'\]\['namod\_toppar'\]  
self.narna\_toppar = self.cfg\['minimization'\]\['narna\_toppar'\]  
self.watio\_toppar = self.cfg\['minimization'\]\['watio\_toppar'\]  
self.modreac\_toppar = self.cfg\['minimization'\]\['modreac\_toppar'\]  
