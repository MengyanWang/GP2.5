

Specify the interpreter and author info
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

# Written by Shikai Jin on 2021-Jun-16, latest modified on 2021-Jun-16
# Add verbose mode
# A greatly expansion of the calculate Q script, now support multiple chains
# Remeber only works for ATOM, not for HETATM
# Example in Linux: python /mnt/e/linux/script/Calculate_Q_value_pdb1_pdb2_var_length.py T1003/3D-JIGSAW_SL1_TS1.pdb T1003_reference_6hrh_A.pdb 0 --start1 30 --end1 465


__AUTHOR__ = 'Shikai Jin'
__DATE__ = '2022-06-11'
__VERSION__ = '1.1'

import argparse
import math
import sys
from Bio.PDB.PDBParser import PDBParser
```
Calculate and return the vector that goes from point 'p1' to point 'p2'.

    p2[0] - p1[0]' calculates the different between the x coordinates of 'p2' and 'p1'; 
    
    p2[1] - p1[1]' calculates the different between the y coordinates of 'p2' and 'p1';
    
    p2[2] - p1[2]' calculates the different between the z coordinates of 'p2' and 'p1'.
    
```
def vector(p1, p2):
    return [p2[0] - p1[0], p2[1] - p1[1], p2[2] - p1[2]]
```
Calculate the magnitude (or length) of a 3D vector 'a' using Pythagorean theorem
```
def vabs(a):
    return math.sqrt(pow(a[0], 2) + pow(a[1], 2) + pow(a[2], 2))
```
Q calculation:
    ca_atoms_pdb1, ca_atoms_pdb2: the two structure for comparison
    q_type: q_type == 0 correspons to the 'CA only' method for calculating the Q,where the contribution of each alpha carbon pair to the Q value is calculated using a Gaussian function with a fixed variance and the 'contact' flag is set to 'False'
            q_type == 1
```
# For the equation of calculate the Q value read dx.doi.org/10.1021/jp212541y
    
def compute_Q_pdb1_pdb2(ca_atoms_pdb1, ca_atoms_pdb2, q_type, sigma_sq, contact, cutoff, minimum_separation):
    Q_value = 0
    count_a = 0
    ca_length = len(ca_atoms_pdb2)
    if q_type == 1:
        minimum_separation = 4
        cutoff = 9.5
        contact = True
    elif q_type == 0:
        minimum_separation = 3
        contact = False  # Temporality save to avoid q=0 and contact=true
        cutoff = 9.5
    elif q_type == 2:
        pass
    else:
        sys.exit("The Q value type %s should be 2, 1 or 0" % q_type)

    if len(ca_atoms_pdb1) != len(ca_atoms_pdb2):
        sys.exit("The number of C alpha atoms in pdb1 file %s doesn't match the number in pdb2 file %s" % (
            len(ca_atoms_pdb1), len(ca_atoms_pdb2)))

    # print(contact)
    # print(cutoff)
    for ia in range(ca_length):
        for ja in range(ia + minimum_separation, ca_length):
            if (ia + 1) in ca_atoms_pdb1 and (ja + 1) in ca_atoms_pdb1:
                rij_N = vabs(
                    vector(ca_atoms_pdb1[ia + 1], ca_atoms_pdb1[ja + 1]))
                rij = vabs(
                    vector(ca_atoms_pdb2[ia + 1], ca_atoms_pdb2[ja + 1]))
                dr = rij - rij_N
                if contact == True:
                    if abs(rij_N) < cutoff:
                        Q_value = Q_value + \
                            math.exp(-dr * dr / (2 * sigma_sq[ja - ia]))
                        count_a = count_a + 1
                else:
                    Q_value = Q_value + \
                        math.exp(-dr * dr / (2 * sigma_sq[ja - ia]))
                    count_a = count_a + 1
    try:
        Q_value = Q_value / count_a
    except:
        Q_value = 0
    return Q_value
    ```











