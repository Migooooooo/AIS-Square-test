## Introduction

This dataset cnontains DFT samples in DeepMD format used in [1], for ferroelectric $\alpha-In_2Se_3$.

## Generation Approach

We use a 20-atom slab model to represent the monolayer system and a 30-atom supercell to model the bulk. DFT calculations are carried out with the Vienna Ab initio Simulation (VASP) package [2,3], employing the projected augmented wave (PAW) method [4,5] and the generalized gradient approximation of Perdew-Burke-Ernzerhof (PBE) [6] type for the exchangecorrelation functional as most of previous first-principles DFT studies of monolayer In2Se3 used PBE. An energy cutoff of 700 eV and a k-point spacing of 0.3 $Å^−1$ (corresponding to a 4 × 4 × 1 k-point mesh for a 20-atom slab model) are sufficient to converge the energy and atomic force. At the exploration step, the configuration space is sampled by running NPT simulations at various temperatures (from 300 to 1200 K) at 0 and 1 kBar, respectively.

## Data Format

The directory tree is as follows:

```
Liugourp
-- database/Liugroup
-- PseudoPotential
```

Subdirectory of database/Liugroup contains unit systems in DeePMD format.

A pbc unit system usually has the following substructure:

```
-- system
-- -- type_map.raw
-- -- type.raw
-- -- set.000/box.npy
-- -- set.000/coord.npy
-- -- set.000/energy.npy
-- -- set.000/force.npy
-- -- set.000/virial.npy
```

Format Description

| Name     | Property           | Raw file     | Unit | Shape                  | Description                                                  |
| -------- | ------------------ | ------------ | ---- | ---------------------- | ------------------------------------------------------------ |
| type     | Atom type indexes  | type.raw     |      | Natoms                 | Integers that start with 0, represent the atomic type corresponding to type_map.raw |
| type_map | Atom type names    | type_map.raw |      | Ntypes                 | Atom names that map to atom type, which is unnecessart to be contained in the periodic table |
| coord    | Atomic coordinates | coord.npy    | Å    | Nframes \* Natoms \* 3 | The atomic coordinates                                       |
| box      | Boxes              | box.npy      | Å    | Nframes \* 3 \* 3      | The box axes in the order `XX XY XZ YX YY YZ ZX ZY ZZ`       |
| energy   | Frame energies     | energy.npy   | eV   | Nframes                | The potential energy of snapshot                             |
| force    | Atomic forces      | force.npy    | eV/Å | Nframes \* Natoms \* 3 | The atomic forces                                            |
| virial   | Frame virial       | virial.npy   | eV   | Nframes * 9            | The virial frames are in the order `XX XY XZ YX YY YZ ZX ZY ZZ` |

Check [here](https://github.com/deepmodeling/deepmd-kit/blob/master/doc/data/system.md) for more details.



## References

[1] Wu, Jing, et al. "Accurate force field of two-dimensional ferroelectrics from deep learning." *Physical Review B* 104.17 (2021): 174107.

[2] Kresse, Georg, and Jürgen Furthmüller. "Efficient iterative schemes for ab initio total-energy calculations using a plane-wave basis set." *Physical review B* 54.16 (1996): 11169.

[3] Kresse, Georg, and Jürgen Furthmüller. "Efficiency of ab-initio total energy calculations for metals and semiconductors using a plane-wave basis set." *Computational materials science* 6.1 (1996): 15-50.

[4] Blöchl, Peter E. "Projector augmented-wave method." *Physical review B* 50.24 (1994): 17953.

[5] Kresse, Georg, and Daniel Joubert. "From ultrasoft pseudopotentials to the projector augmented-wave method." *Physical review b* 59.3 (1999): 1758.

[6] Perdew, John P., Kieron Burke, and Matthias Ernzerhof. "Generalized gradient approximation made simple." *Physical review letters* 77.18 (1996): 3865.
