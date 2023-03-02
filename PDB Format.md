# PDB Format
Column **1-6**: ATOM

Column **7-11**: Atom Serial Number

Column **13-16**: Atom name:4 letter code that identify the type of atom (e.g.,"CA" for alpha carbon)

Column **17**: Alternate locaiton indicator: is used when there are multiple conformations of an atom in the structure

Column **18-20**:Residue name

Column **22**:Chain identifier: identifies the polypeptide chain to which the residue belongs

Column **23-26**:Residue sequence number

Column **27**: Code for insertion of residues: is used when residues are added to a structure after it has been solved

Column **31-38**: X orthogonal angstom coordinate

Column **39-46**: Y orthogonal angstom coordinate

Column **47-54**: Z orthognonal angstom coordinate

Column **55-60**: Occupancy: represents the fraction of unit cell occupied by the atom

Column **61-66**: Temperature factor: represents the thermal motion if the atom

Column **73-76**: Segment identifier: is obsolete but still used by some programs.Chimera assigns it as the atom attribute pdbSegment to allow command-line specification

Column **77-78**: Element Symbol: identifies the type of atom based on its atomic number(C for carbon)````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````

Column **79-80**: Charge: charge on the atom

