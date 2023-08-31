---
title: vaspkit-教程翻译（input）
abbrlink: b9df750d
date: 2023-08-30 21:57:57
categories: 
- vaspkit
tags:
- vaspkit
- input
- KPOINTS
- INCAR
- POSCAR
- POTCAR
--- 
# vaspkit英文版教程-译

## 教程

该教程作为一个完整的输入仅提供常见输入示例，不保证科学性和精度，一些参数需要使用者自己修改。

## 快速开始

### 你可以启动的方式

使用vaspkit至少有五种方式，在这里我们以产生K点文件（102）为例进行演示。

- 1、在终端中键入`vaspkit`启动；

- 2、`vaspkit -task 102 -kpr 0.04` 使用2π × 0.04 Å<sup>-1</sup>的倒空间方案产生K点，使用`vasplit - help`获得更多细节，**请注意该功能还未被支持。**；
- 3、 使用命令：`echo -e "102\n2\n0.04\n"| vaspkit`;
- 4、使用命令： `(echo 102; echo 2; echo 0.04)|vaspkit`;
- 5、编辑一个filename的文本文件，里面需要包括以下内容

```
102
2
0.04
```

然后运行以下命令：`vaspkit filename` 。
### 批处理模式运行 `vaspkit`

如果你想以批处理模式运行 `vaspkit` ，例如你想在一些子文件夹中使用 `vaspkit` 产生KPOINTS，

```
for i in `ls`
do echo ${i}
    cd ${i}
    echo -e "102\n2\n0.04" | vaspkit 
    # vaspkit -task 102 -file POSCAR -kpr 0.04
    # 因为在上述运行的五种方式中方式2目前还不支持，我们用方式3来代替该命令。
    cd ..
done
```
此为这种结构下产生KPOINTS的批处理命令

```
lianxi
├── 01
│   ├── INCAR
│   ├── POSCAR
│   └── Si.cif
├── 02
│   ├── INCAR
│   ├── POSCAR
└── 03
│   ├── INCAR
│   ├── POSCAR
```

因此我们就可以在根文件夹下运行上述批处理命令：屏幕显示这样：

```
01


            \\\///
           / _  _ \         Hey, you must know what you are doing.
         (| (o)(o) |)       Otherwise you might get wrong results.
 +-----.OOOo--()--oOOO.------------------------------------------+
 |         VASPKIT Standard Edition 1.3.5 (03 Jul. 2022)         |
 |         Core Developer: Vei WANG (wangvei@icloud.com)         |
 |     Main Contributors: Nan XU, Jin-Cheng LIU & Gang TANG      |
 |  Online Tutorials Available on Website: https://vaspkit.com   |
 +-----.oooO-----------------------------------------------------+
        (   )   Oooo.                          VASPKIT Made Simple
         \ (    (   )
          \_)    ) /
                (_/
 ===================== Structural Utilities ======================
 1)  VASP Input-Files Kit          2)  Mechanical Properties
 3)  K-Path for Band-Structure     4)  Structure Editor
 5)  Catalysis-ElectroChem Kit     6)  Symmetry Analysis
 8)  Advanced Structure Models
 ===================== Electronic Utilities ======================
 11) Density-of-States             21) Band-Structure
 23) 3D Band-Structure             25) Hybrid-DFT Band-Structure
 26) Fermi-Surface                 28) Band-Structure Unfolding
 31) Charge-Density Analysis       42) Potential Analysis
 51) Wave-Function Analysis        62) Magnetic Properties
 65) Spin-Texture                  68) Transport Properties
 ======================== Misc Utilities =========================
 71) Optical Properties            72) Molecular-Dynamics Kit
 74) User Interface                78) VASP2other Interface
 91) Semiconductor Kit             92) 2D-Material Kit
 0)  Quit
 ------------>>
 ======================== K-Mesh Scheme ==========================
 1) Monkhorst-Pack Scheme
 2) Gamma Scheme
 3) Irreducible K-Points with Gamma Scheme

 0)   Quit
 9)   Back
 ------------->>
 -->> (01) Reading Structural Parameters from POSCAR File...
 +-------------------------- Warm Tips --------------------------+
   * Accuracy Levels: Gamma-Only: 0;
                      Low: 0.06~0.04;
                      Medium: 0.04~0.03;
                      Fine: 0.02-0.01.
   * 0.03-0.04 is Generally Precise Enough!
 +---------------------------------------------------------------+
 Input Kmesh-Resolved Value (in Units of 2*PI/Angstrom):
 ------------>>
 +-------------------------- Summary ----------------------------+
 Reciprocal Lattice Vectors (in Units of 1/Angstrom):
       1.1569752163       0.0000000000       0.0000000000
       0.0000000000       1.1569752163       0.0000000000
       0.0000000000       0.0000000000       1.1569752163
 Reciprocal Lattice Constants:   1.1570   1.1570   1.1570
 Real-Space Lattice Constants:   5.4307   5.4307   5.4307
 K-Mesh Size:    5    5    5
 +---------------------------------------------------------------+
 -->> (02) Written KPOINTS File!
 +---------------------------------------------------------------+
 |                       * ACKNOWLEDGMENTS *                     |
 | Other Contributors (in no particular order): Peng-Fei LIU,    |
 | Xue-Fei LIU, Dao-Xiong WU, Zhao-Fu ZHANG, Tian WANG, Qiang LI,|
 | Ya-Chao LIU, Jiang-Shan ZHAO, Qi-Jing ZHENG, Yue QIU and You! |
 | Advisors: Wen-Tong GENG, Yoshiyuki KAWAZOE                    |
 | Any Suggestions for Improvement are Welcome and Appreciated!  |
 +---------------------------------------------------------------+
 |                          * CITATIONS *                        |
 | When using VASPKIT in your research PLEASE cite the paper:    |
 | [1] V. WANG, N. XU, J.-C. LIU, G. TANG, W.-T. GENG, VASPKIT: A|
 | User-Friendly Interface Facilitating High-Throughput Computing|
 | and Analysis Using VASP Code, Computer Physics Communications |
 | 267, 108033, (2021), DOI: 10.1016/j.cpc.2021.108033           |
 +---------------------------------------------------------------+
02


            \\\///
           / _  _ \         Hey, you must know what you are doing.
         (| (o)(o) |)       Otherwise you might get wrong results.
 +-----.OOOo--()--oOOO.------------------------------------------+
 |         VASPKIT Standard Edition 1.3.5 (03 Jul. 2022)         |
 |         Core Developer: Vei WANG (wangvei@icloud.com)         |
 |     Main Contributors: Nan XU, Jin-Cheng LIU & Gang TANG      |
 |  Online Tutorials Available on Website: https://vaspkit.com   |
 +-----.oooO-----------------------------------------------------+
        (   )   Oooo.                          VASPKIT Made Simple
         \ (    (   )
          \_)    ) /
                (_/
 ===================== Structural Utilities ======================
 1)  VASP Input-Files Kit          2)  Mechanical Properties
 3)  K-Path for Band-Structure     4)  Structure Editor
 5)  Catalysis-ElectroChem Kit     6)  Symmetry Analysis
 8)  Advanced Structure Models
 ===================== Electronic Utilities ======================
 11) Density-of-States             21) Band-Structure
 23) 3D Band-Structure             25) Hybrid-DFT Band-Structure
 26) Fermi-Surface                 28) Band-Structure Unfolding
 31) Charge-Density Analysis       42) Potential Analysis
 51) Wave-Function Analysis        62) Magnetic Properties
 65) Spin-Texture                  68) Transport Properties
 ======================== Misc Utilities =========================
 71) Optical Properties            72) Molecular-Dynamics Kit
 74) User Interface                78) VASP2other Interface
 91) Semiconductor Kit             92) 2D-Material Kit
 0)  Quit
 ------------>>
 ======================== K-Mesh Scheme ==========================
 1) Monkhorst-Pack Scheme
 2) Gamma Scheme
 3) Irreducible K-Points with Gamma Scheme

 0)   Quit
 9)   Back
 ------------->>
 -->> (01) Reading Structural Parameters from POSCAR File...
 +-------------------------- Warm Tips --------------------------+
   * Accuracy Levels: Gamma-Only: 0;
                      Low: 0.06~0.04;
                      Medium: 0.04~0.03;
                      Fine: 0.02-0.01.
   * 0.03-0.04 is Generally Precise Enough!
 +---------------------------------------------------------------+
 Input Kmesh-Resolved Value (in Units of 2*PI/Angstrom):
 ------------>>
 +-------------------------- Summary ----------------------------+
 Reciprocal Lattice Vectors (in Units of 1/Angstrom):
       1.1569752163       0.0000000000       0.0000000000
       0.0000000000       1.1569752163       0.0000000000
       0.0000000000       0.0000000000       1.1569752163
 Reciprocal Lattice Constants:   1.1570   1.1570   1.1570
 Real-Space Lattice Constants:   5.4307   5.4307   5.4307
 K-Mesh Size:    5    5    5
 +---------------------------------------------------------------+
 -->> (02) Written KPOINTS File!
 -->> (03) Written INCAR file!
 +-------------------------- Summary ----------------------------+
 POTCAR Type: PBE
 Number of Elements: 1
 POTCAR File No.1: [ POTCAR_Si ], Valence Electron: 4.0
 Total Atoms: 8
 Total Valence Electrons: 32.0
 +---------------------------------------------------------------+
 -->> (04) Written POTCAR File with the Recommended Potential!
 +---------------------------------------------------------------+
 |                       * ACKNOWLEDGMENTS *                     |
 | Other Contributors (in no particular order): Peng-Fei LIU,    |
 | Xue-Fei LIU, Dao-Xiong WU, Zhao-Fu ZHANG, Tian WANG, Qiang LI,|
 | Ya-Chao LIU, Jiang-Shan ZHAO, Qi-Jing ZHENG, Yue QIU and You! |
 | Advisors: Wen-Tong GENG, Yoshiyuki KAWAZOE                    |
 | Any Suggestions for Improvement are Welcome and Appreciated!  |
 +---------------------------------------------------------------+
 |                          * CITATIONS *                        |
 | When using VASPKIT in your research PLEASE cite the paper:    |
 | [1] V. WANG, N. XU, J.-C. LIU, G. TANG, W.-T. GENG, VASPKIT: A|
 | User-Friendly Interface Facilitating High-Throughput Computing|
 | and Analysis Using VASP Code, Computer Physics Communications |
 | 267, 108033, (2021), DOI: 10.1016/j.cpc.2021.108033           |
 +---------------------------------------------------------------+
03


            \\\///
           / _  _ \         Hey, you must know what you are doing.
         (| (o)(o) |)       Otherwise you might get wrong results.
 +-----.OOOo--()--oOOO.------------------------------------------+
 |         VASPKIT Standard Edition 1.3.5 (03 Jul. 2022)         |
 |         Core Developer: Vei WANG (wangvei@icloud.com)         |
 |     Main Contributors: Nan XU, Jin-Cheng LIU & Gang TANG      |
 |  Online Tutorials Available on Website: https://vaspkit.com   |
 +-----.oooO-----------------------------------------------------+
        (   )   Oooo.                          VASPKIT Made Simple
         \ (    (   )
          \_)    ) /
                (_/
 ===================== Structural Utilities ======================
 1)  VASP Input-Files Kit          2)  Mechanical Properties
 3)  K-Path for Band-Structure     4)  Structure Editor
 5)  Catalysis-ElectroChem Kit     6)  Symmetry Analysis
 8)  Advanced Structure Models
 ===================== Electronic Utilities ======================
 11) Density-of-States             21) Band-Structure
 23) 3D Band-Structure             25) Hybrid-DFT Band-Structure
 26) Fermi-Surface                 28) Band-Structure Unfolding
 31) Charge-Density Analysis       42) Potential Analysis
 51) Wave-Function Analysis        62) Magnetic Properties
 65) Spin-Texture                  68) Transport Properties
 ======================== Misc Utilities =========================
 71) Optical Properties            72) Molecular-Dynamics Kit
 74) User Interface                78) VASP2other Interface
 91) Semiconductor Kit             92) 2D-Material Kit
 0)  Quit
 ------------>>
 ======================== K-Mesh Scheme ==========================
 1) Monkhorst-Pack Scheme
 2) Gamma Scheme
 3) Irreducible K-Points with Gamma Scheme

 0)   Quit
 9)   Back
 ------------->>
 -->> (01) Reading Structural Parameters from POSCAR File...
 +-------------------------- Warm Tips --------------------------+
   * Accuracy Levels: Gamma-Only: 0;
                      Low: 0.06~0.04;
                      Medium: 0.04~0.03;
                      Fine: 0.02-0.01.
   * 0.03-0.04 is Generally Precise Enough!
 +---------------------------------------------------------------+
 Input Kmesh-Resolved Value (in Units of 2*PI/Angstrom):
 ------------>>
 +-------------------------- Summary ----------------------------+
 Reciprocal Lattice Vectors (in Units of 1/Angstrom):
       1.1569752163       0.0000000000       0.0000000000
       0.0000000000       1.1569752163       0.0000000000
       0.0000000000       0.0000000000       1.1569752163
 Reciprocal Lattice Constants:   1.1570   1.1570   1.1570
 Real-Space Lattice Constants:   5.4307   5.4307   5.4307
 K-Mesh Size:    5    5    5
 +---------------------------------------------------------------+
 -->> (02) Written KPOINTS File!
 -->> (03) Written INCAR file!
 +-------------------------- Summary ----------------------------+
 POTCAR Type: PBE
 Number of Elements: 1
 POTCAR File No.1: [ POTCAR_Si ], Valence Electron: 4.0
 Total Atoms: 8
 Total Valence Electrons: 32.0
 +---------------------------------------------------------------+
 -->> (04) Written POTCAR File with the Recommended Potential!
 +---------------------------------------------------------------+
 |                       * ACKNOWLEDGMENTS *                     |
 | Other Contributors (in no particular order): Peng-Fei LIU,    |
 | Xue-Fei LIU, Dao-Xiong WU, Zhao-Fu ZHANG, Tian WANG, Qiang LI,|
 | Ya-Chao LIU, Jiang-Shan ZHAO, Qi-Jing ZHENG, Yue QIU and You! |
 | Advisors: Wen-Tong GENG, Yoshiyuki KAWAZOE                    |
 | Any Suggestions for Improvement are Welcome and Appreciated!  |
 +---------------------------------------------------------------+
 |                          * CITATIONS *                        |
 | When using VASPKIT in your research PLEASE cite the paper:    |
 | [1] V. WANG, N. XU, J.-C. LIU, G. TANG, W.-T. GENG, VASPKIT: A|
 | User-Friendly Interface Facilitating High-Throughput Computing|
 | and Analysis Using VASP Code, Computer Physics Communications |
 | 267, 108033, (2021), DOI: 10.1016/j.cpc.2021.108033           |
 +---------------------------------------------------------------+
```
最后文件拓扑为：
```
lianxi/
├── 01
│   ├── INCAR
│   ├── KPOINTS
│   ├── POSCAR
│   ├── POTCAR
│   └── Si.cif
├── 02
│   ├── INCAR
│   ├── KPOINTS
│   ├── POSCAR
│   └── POTCAR
└── 03
    ├── INCAR
    ├── KPOINTS
    ├── POSCAR
    └── POTCAR
```
使用 `echo -e "102\n2\n0.04" | vaspkit` 运行 `vaspkit` 意味着在 `vaspkit` 中键入  `102，2，0.04`  。
如果你想得到其他的物理性质，也可以通过批处理命令来实现，比如得到子文件夹中的带隙：

```
# 代码已测试，另本人已修改
# 适用版本如下：
# VASPKIT Standard Edition 1.3.5 (03 Jul. 2022)
for i in `ls`
do echo ${i}
    cd ${i}
    echo -e "911\n" | vaspkit | sed -n '45p' | awk '{print $4}'
    cd ..
done
```
### 生成INPUT文件
为了运行 `vasp` 你需要四个输入文件，即 `INCAR、KPOINTS、POSCAR、POTCAR`.
- 1、`INCAR` 包括所有的关键词，主要是告诉 `vasp` 计算什么内容。
- 2、`KPOINTS` 他可以包括在 `INCAR` 中，但是不建议省略。它包括倒空间中的K点信息，用于插值计算波函数获得电子密度。
- 3、`POSCAR` 包括晶格常数，原子笛卡尔坐标（或分数坐标），原子速度信息（用于分子动力学计算）。
- 4、`POTCAR` 是一个赝势文件，可以是超软赝势（USPP）或者投影缀加平面波(PAW)。
运行 `vaspkit 1` :

```
==================== VASP Input Files Options ===================
 101) Customize INCAR File
 102) Generate KPOINTS File for SCF Calculation
 103) Generate POTCAR File with Default Setting
 104) Generate POTCAR File with User Specified Potential
 105) Generate POSCAR File from cif (no fractional occupations)
 106) Generate POSCAR File from Material Studio xsd (retain fixes)
 107) Reformat POSCAR File in Specified Order of Elements
 108) Successive Procedure to Generate VASP Files and Check
 109) Submit Job Queue
```

### 生成INCAR
在包含 `POSCAR` 的文件夹中运行 `vaspkit` ，然后输入 `1` 选择要生成的 `vasp` 输入文件类型，然后键入 `101` 进入自定义选择 `INCAR` 类型，你将得到以下视图：

```
+-------------------------- Warm Tips --------------------------+
                You MUST Know What You Are doing
  Some Parameters in INCAR File Neet To Be Set/Adjusted Manually
 +---------------------------------------------------------------+
 ======================== INCAR Options ==========================
 ST) Static-Calculation            SR) Standard Relaxation
 MG) Magnetic Properties           SO) Spin-Orbit Coupling
 D3) DFT-D3 no-damping Correction  H6) HSE06 Calculation
 PU) DFT+U Calculation             MD) Molecular Dynamics
 GW) GW0 Calculation               BS) BSE Calculation
 DC) Elastic Constant              EL) ELF Calculation
 BD) Bader Charge Analysis         OP) Optical Properties
 EC) Static Dielectric Constant    PC) Decomposed Charge Density
 FD) Phonon-Finite-Displacement    DT) Phonon-DFPT
 NE) Nudged Elastic Band (NEB)     DM) The Dimer Method
 FQ) Frequence Calculations        LR) Lattice Relaxation
```

键入特定任务的关键词，将会生成包含相关关键词的 `INCAR` 文件。
例如，你要使用杂化泛函计算带有DFT-D3色散矫正的单点任务，那么你可以键入 `STH6D3` 。
例如键入  `LR` ，将会得到一个具有详细晶格弛豫参数的 `INCAR` ：

```
Global Parameters
ISTART =  1            (Read existing wavefunction, if there)
ISPIN  =  1            (Non-Spin polarised DFT)
# ICHARG =  11         (Non-self-consistent: GGA/LDA band structures)
LREAL  = .FALSE.       (Projection operators: automatic)
# ENCUT  =  400        (Cut-off energy for plane wave basis set, in eV)
# PREC   =  Accurate   (Precision level: Normal or Accurate, set Accurate when perform structure lattice relaxation calculation)
LWAVE  = .TRUE.        (Write WAVECAR or not)
LCHARG = .TRUE.        (Write CHGCAR or not)
ADDGRID= .TRUE.        (Increase grid, helps GGA convergence)
# LVTOT  = .TRUE.      (Write total electrostatic potential into LOCPOT or not)
# LVHAR  = .TRUE.      (Write ionic + Hartree electrostatic potential into LOCPOT or not)
# NELECT =             (No. of electrons: charged cells, be careful)
# LPLANE = .TRUE.      (Real space distribution, supercells)
# NWRITE = 2           (Medium-level output)
# KPAR   = 2           (Divides k-grid into separate groups)
# NGXF    = 300        (FFT grid mesh density for nice charge/potential plots)
# NGYF    = 300        (FFT grid mesh density for nice charge/potential plots)
# NGZF    = 300        (FFT grid mesh density for nice charge/potential plots)

Lattice Relaxation
NSW    =  300          (number of ionic steps)
ISMEAR =  0            (gaussian smearing method )
SIGMA  =  0.05         (please check the width of the smearing)
IBRION =  2            (Algorithm: 0-MD, 1-Quasi-New, 2-CG)
ISIF   =  3            (optimize atomic coordinates and lattice parameters)
EDIFFG = -1.5E-02      (Ionic convergence, eV/A)
PREC   =  Accurate     (Precision level)
```
如果您是一个老司机，想要得到更加干净的 `INCAR` 文件，可以修改 `~/.vaspkit` 中的 `MINI_INCAR` 选项，将其设置为 `.TRUE.` ，这样生成的用于晶格弛豫计算的 `INCAR` 将会是：
```
Global Parameters
  ISTART = 1
  LREAL = Auto
  PREC = Normal
  LWAVE = .TRUE.
  LCHARG = .TRUE.
  ADDGRID= .TRUE.

Lattice Relaxation
  NSW = 300
  ISMEAR = 0
  SIGMA = 0.05
  IBRION = 2
  ISIF = 3
  EDIFFG = -1.5E-02
  PREC = Accurat
```
使用者仍然可以按照他们的需要修改新生成的输入文件中的参数。
> **Notes:
>如果你的文件中本来由一个 `INCAR` ，您仍然使用 `vaspkit` 生成 `INCAR` ,则原来的 `INCAR` 文件将会被自动覆盖；您可以通过简单修改   `~/.vaspkit` 中的 `SET_INCAR_WRITE_MODE` 选项来修改 `INCAR` 的输出选项；具体参数如下：
>`OVERRICE` : ` 新的内容添加到原来的 `INCAR` 之后` ;
>`APPEND`  : `新生成的内容添加到旧的 `INCAR` 之后` ;
>`BACK-UP-OLD` : `备份新的 `INCAR` ;
>`BACK-UP-NEW` :  `将新生成的 `INCAR` 作为使用的 `INCAR` 。

### 生成K点文件
为了自洽运算，用户需要准备一个特定密度和自动产生 `K` 点方法的 `KPOINTS` 文件。
如果当前文件夹中已有 `POSCAR` ，则 `vaspkit` 可以根据已经存在的  `POSCAR` 文件自动生成  `KPOINTS` 文件。运行 `vaspkit` 的选项 `1) VASP Input Files Generator` ，然后键入 `102` 生成自洽循环的  `KPOINTS` 文件，然后根据以下展示的信息选择 `K-mesh` 方案：

```
 ======================== K-Mesh Scheme ==========================
 1) Monkhorst-Pack Scheme
 2) Gamma Scheme
 3) Irreducible K-Points with Gamma Scheme

 0)   Quit
 9)   Back
 ------------->>
```
键入 `1` 选择原始的 `Monkhorst-Pack` 方案；
键入 `2` 选择以 `Gamma` 为中心的 `Monkhorst-Pack` 方案。
接着， `vaspkit` 将会要求我们在倒空间中输入 `K-POINTS` 之间 `KPT` 的解析值，单位为 2π×0.04Å<sup>−1</sup> 。

```
2
  -->> (01) Reading Structural Parameters from POSCAR File...
 +-------------------------- Warm Tips --------------------------+

 * Accuracy Levels: Gamma-Only: 0;
    Low: 0.06~0.04;
    Medium: 0.04~0.03;
    Fine: 0.02-0.01.
 * 0.03-0.04 is Generally Precise Enough!
   +---------------------------------------------------------------+
    Input KPT-Resolved Value (e.g., 0.04, in unit of 2*PI/Angstrom):
    ------------>>
```
`K-POINTS` 的数量随着 ` KPT-resolved value (kpr)` 的减少；如果 ` KPT-resolved value (kpr)` 增加则 `K-POINTS` 的数量减少。对于每一个方向，数量由 N = max(1,|b<sub>i</sub>|/kpr) 决定，b<sub>i</sub>是倒晶格的格矢，其值将舍入到下一个大于或等于 `N` 的整数，对于大多数系统来说，这个值取 `0.04` 已经足够了，这个参数像 `INCAR` 中的 `KSPACING` ，但是他们的单位不同， `KSACING` 的单位是 Å<sup>−1</sup>，而 `vaspkit`  的单位是 2π × 0.04 Å<sup>−1</sup>。
输出的 `KPOINTS` 文件的第一行是用户定义的 `KPT` 的解析值：

```
K-Mesh Generated with KP-Resolved Value (...): 0.020
0
Gamma
  14  14  14
0.0  0.0  0.0
```
### 生成POTCAR
当用 `vaspkit` 产生 `KPOINTS` 时，将会自动产生 `POSCAR` 对应的 `POTCAR` 文件，或者用 `vaspkit` 的 `103` 功能产生。

```
103
  -->> (01) Reading Structural Parameters from POSCAR File...
  -->> (02) Written POTCAR File with the Standard Potential!
```
它自动从 `POSCAR` 中读取元素并从你在 `~/.vaspkit` 中设置的赝势库中选择对应的赝势写入 `POTCAR` 中。

```
GGA_PATH                 '~/POTCAR/GGA'     #  Path of GGA potential.
PBE_PATH                 '~/POTCAR/PBE'     #  Path of PBE potential.
LDA_PATH                 '~/POTCAR/LDA'     #  Path of LDA potential.
POTCAR_TYPE               PBE               #  PBE, GGA or LDA;
RECOMMENDED_POTCAR       .TRUE.             # .TRUE. or .FALSE.;
```
设置你所想用的赝势类型，可选项为：`LDA、GGA、PBE` ，选项 `RECOMMENDED_POTCAR` 控制你是否需要使用 `vasp` 手册中推荐的赝势类型(Page. 195, 2018.10.29, [http://cms.mpi.univie.ac.at/vasp/vasp/Recommended_PAW_potentials_DFT_calculations_using_vasp_5_2.html](http://cms.mpi.univie.ac.at/vasp/vasp/Recommended_PAW_potentials_DFT_calculations_using_vasp_5_2.html))。
如果该选项为 `False` ，那么将使用没有扩展的赝势使用；如果该选项为 `True` ，那么将使用手册推荐的赝势类型。
**赝势类型：
- 无扩展的， “ _ ”   ；
-  `_d`, 将d的半核当作价层处理 ；
- `_pv` or `_sv` ，将_p和__s_半核状态被视为价态 ；
- `_h` and `_s` ， 电位比标准电位更硬或更软，因此需要更高或更低的截断能量 ；
- 赝势氢原子：`H_5` ；
- `_GW` , 用于 `GW`  计算 。
如果你想产生用于 `GW` 计算的 `POTCAR` 文件，只需要将 `~/.vaspkit` 中的 `GW_POTCAR` 选项设置为 `True` 即可：
`GW_POTCAR                .TRUE.            # .TRUE. or .FALSE.;`
`vaspkit` 也提供手动为每一个元素类型设置 `POTCAR` ，可以通过 `104` 选项实现。

```
104
 -->> (1) Reading Structural Parameters from POSCAR File...
 Auto detected POTCAR_TYPE is O, please type the one you want!
O_h
 Auto detected POTCAR_TYPE is Ti, please type the one you want!
Ti_sv
 -->> (2) Written POTCAR File with user specified Potential!
```
比如在这个例子中，用户要为 `Ti` 和 `O` 选择赝势为 `Ti` 和 `O` ，因为不在数据库中，`vaspkit` 将会智能提示你重新输入 `Ti_sv` 和 `O_h` 。
### 生成POSCAR
`vaspkit` 可以通过 `.cif` [105功能] 和 `.xsd` (materials studio 文件类型)[106功能]来生成 `POSCAR` 。
`105` 功能将唤醒脚本 `/vaspkit.1.00/utilities/cif2pos.py` 。

```
105
 Please type in the filename of cif->
al2o3.cif
Pleas input the order of element, `ENTER` for default!
Example: 'Al O' in this CIF

  -->> (01) POSCAR has been generated...
```
`106` 将会运行脚本`/vaspkit.1.00/utilities/xsd2pos.py` ,该脚本能够自动识别 `.xsd` 中的原子固定信息并正确转化为具有正确固定原子信息的 `POSCAR` 。
`107` 功能可以按照用户指定的元素种类顺序重新排列元素：

```
107
 -->> (01) Reading Structural Parameters from POSCAR File...
 Please Type the New Order of Elements to Sort.
 (Tip: The Initial Order of Elements in POSCAR File is:  C Fe  N  H)
 ------------->>
```
### 输入文件自检
`vaspkit` 可以通过 `109` 功能来检查赝势和进行格式校正，同时其将自动校正 `INCAR` 和 `POSCAR` ，并检查 `POTCAR` 和 `POSCAR` 元素顺序是否一致。