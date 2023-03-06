

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
