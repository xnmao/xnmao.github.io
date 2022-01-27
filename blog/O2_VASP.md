---
layout: default
---

### 计算细节

#### H2O
##### 弛豫
###### INCAR
```shell
INCAR created by Atomic Simulation Environment
 ENCUT = 520.000000
 SIGMA = 0.050000
 EDIFFG = -3.00e-02
 ALGO = Fast
 GGA = PE
 PREC = Normal
 IBRION = 2
 ISMEAR = 0
 NSW = 1000
 LCHARG = .FALSE.
 LWAVE = .FALSE.
 LREAL = .FALSE.
```
###### KPOINTS
```shell
KPOINTS created by Atomic Simulation Environment
0
Gamma
1 1 1 
0 0 0
```
###### CONTCAR
```shell
 H  O                                   
   1.00000000000000     
    15.0000000000000000    0.0000000000000000    0.0000000000000000
     0.0000000000000000   15.0000000000000000    0.0000000000000000
     0.0000000000000000    0.0000000000000000   15.0000000000000000
   H    O 
     2     1
Direct
  0.5000000000000000  0.5511700331925511  0.4801208237006717
  0.5000000000000000  0.4488299668074490  0.4801208237006717
  0.5000000000000000  0.5000000000000000  0.5198813859319917
 
  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00
```
###### 基态电子能量
```shell
$ tail -1 vasp.out
 reached required accuracy - stopping structural energy minimisation
$ grep sigma OUTCAR | tail -1
  energy  without entropy=      -14.21977328  energy(sigma->0) =      -14.21977328
```

##### 振动
###### INCAR
```shell
INCAR created by Atomic Simulation Environment
 ENCUT = 520.000000
 POTIM = 0.015000
 SIGMA = 0.050000
 ALGO = Fast
 GGA = PE
 PREC = Normal
 IBRION = 5
 ISMEAR = 0
 NELM = 999
 NFREE = 2
 NSW = 1
 LCHARG = .FALSE.
 LWAVE = .FALSE.
 LREAL = .FALSE.
```
###### 振动频率
```shell
$ grep meV OUTCAR
   1 f  =  115.217449 THz   723.932586 2PiTHz 3843.240310 cm-1   476.501240 meV
   2 f  =  111.923744 THz   703.237623 2PiTHz 3733.374124 cm-1   462.879564 meV
   3 f  =   47.564240 THz   298.854937 2PiTHz 1586.572235 cm-1   196.709957 meV
   4 f  =    1.551205 THz     9.746511 2PiTHz   51.742639 cm-1     6.415272 meV
   5 f  =    0.316558 THz     1.988991 2PiTHz   10.559228 cm-1     1.309178 meV
   6 f/i=    0.012925 THz     0.081213 2PiTHz    0.431147 cm-1     0.053455 meV
   7 f/i=    1.247288 THz     7.836941 2PiTHz   41.605047 cm-1     5.158370 meV
   8 f/i=    2.219820 THz    13.947542 2PiTHz   74.045231 cm-1     9.180442 meV
   9 f/i=    2.632461 THz    16.540241 2PiTHz   87.809449 cm-1    10.886988 meV
```

#### H2
##### 弛豫
###### INCAR
```shell
INCAR created by Atomic Simulation Environment
 ENCUT = 520.000000
 SIGMA = 0.050000
 EDIFFG = -3.00e-02
 ALGO = Fast
 GGA = PE
 PREC = Normal
 IBRION = 2
 ISMEAR = 0
 NSW = 1000
 LCHARG = .FALSE.
 LWAVE = .FALSE.
 LREAL = .FALSE.
```
###### KPOINTS
```shell
KPOINTS created by Atomic Simulation Environment
0
Gamma
1 1 1 
0 0 0
```
###### CONTCAR
```shell
 H                                      
   1.00000000000000     
    15.0000000000000000    0.0000000000000000    0.0000000000000000
     0.0000000000000000   15.0000000000000000    0.0000000000000000
     0.0000000000000000    0.0000000000000000   15.0000000000000000
   H 
     2
Direct
  0.5000000000000000  0.5000000000000000  0.5250084864229504
  0.5000000000000000  0.5000000000000000  0.4749915135770496
 
  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00
```
###### 基态电子能量
```shell
$ tail -1 vasp.out
 reached required accuracy - stopping structural energy minimisation
$ grep sigma OUTCAR | tail -1
  energy  without entropy=       -6.77111859  energy(sigma->0) =       -6.77111859
```

##### 振动
###### INCAR
```shell
INCAR created by Atomic Simulation Environment
 ENCUT = 520.000000
 POTIM = 0.015000
 SIGMA = 0.050000
 ALGO = Fast
 GGA = PE
 PREC = Normal
 IBRION = 5
 ISMEAR = 0
 NELM = 999
 NFREE = 2
 NSW = 1
 LCHARG = .FALSE.
 LWAVE = .FALSE.
 LREAL = .FALSE.
```
###### 振动频率
```shell
$ grep meV OUTCAR
   1 f  =  129.946185 THz   816.475959 2PiTHz 4334.538025 cm-1   537.414415 meV
   2 f  =    1.532109 THz     9.626522 2PiTHz   51.105639 cm-1     6.336294 meV
   3 f  =    1.499962 THz     9.424540 2PiTHz   50.033348 cm-1     6.203347 meV
   4 f/i=    0.000022 THz     0.000139 2PiTHz    0.000739 cm-1     0.000092 meV
   5 f/i=    0.003081 THz     0.019359 2PiTHz    0.102776 cm-1     0.012743 meV
   6 f/i=    0.031434 THz     0.197507 2PiTHz    1.048535 cm-1     0.130002 meV
```

#### O2
##### 弛豫
###### INCAR
```shell
INCAR created by Atomic Simulation Environment
 ENCUT = 520.000000
 SIGMA = 0.050000
 EDIFFG = -3.00e-02
 ALGO = Fast
 GGA = PE
 PREC = Normal
 IBRION = 2
 ISMEAR = 0
 ISPIN = 2
 LORBIT = 10
 NSW = 1000
 LCHARG = .FALSE.
 LWAVE = .FALSE.
 LREAL = .FALSE.
 MAGMOM = 2*1.0000 
```
###### KPOINTS
```shell
KPOINTS created by Atomic Simulation Environment
0
Gamma
1 1 1 
0 0 0
```
###### CONTCAR
```shell
 O                                      
   1.00000000000000     
    15.0000000000000000    0.0000000000000000    0.0000000000000000
     0.0000000000000000   15.0000000000000000    0.0000000000000000
     0.0000000000000000    0.0000000000000000   15.0000000000000000
   O 
     2
Direct
  0.5000000000000000  0.5000000000000000  0.5410865744056789
  0.5000000000000000  0.5000000000000000  0.4589134255943211
 
  0.00000000E+00  0.00000000E+00  0.00000000E+00
  0.00000000E+00  0.00000000E+00  0.00000000E+00
```
###### 基态电子能量
```shell
$ tail -1 vasp.out
 reached required accuracy - stopping structural energy minimisation
$ grep sigma OUTCAR | tail -1
  energy  without entropy=       -9.85989701  energy(sigma->0) =       -9.85989701
```

##### 振动
###### INCAR
```shell
INCAR created by Atomic Simulation Environment
 ENCUT = 520.000000
 POTIM = 0.015000
 SIGMA = 0.050000
 ALGO = Fast
 GGA = PE
 PREC = Normal
 IBRION = 5
 ISMEAR = 0
 ISPIN = 2
 LORBIT = 10
 NELM = 999
 NFREE = 2
 NSW = 1
 LCHARG = .FALSE.
 LWAVE = .FALSE.
 LREAL = .FALSE.
 MAGMOM = 2*1.0000 
```
###### 振动频率
```shell
$ grep meV OUTCAR
   1 f  =   47.063643 THz   295.709591 2PiTHz 1569.874107 cm-1   194.639653 meV
   2 f  =    0.692483 THz     4.350999 2PiTHz   23.098745 cm-1     2.863880 meV
   3 f  =    0.683547 THz     4.294852 2PiTHz   22.800668 cm-1     2.826924 meV
   4 f/i=    0.000421 THz     0.002644 2PiTHz    0.014038 cm-1     0.001741 meV
   5 f/i=    0.001738 THz     0.010919 2PiTHz    0.057968 cm-1     0.007187 meV
   6 f/i=    0.003568 THz     0.022418 2PiTHz    0.119016 cm-1     0.014756 meV
```

[[Back]](./O2.md)
