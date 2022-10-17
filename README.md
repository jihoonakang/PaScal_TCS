# PaScaL_TCS

Parallel and Scalable Library for Turbulent Convection Solver

The PaScal TCS is an efficient and scalable solver for large-scale direct numerical simulations of turbulent convective
flows, considering temperature-dependent fluid properties. In order to increase scalability on a massive-scale
distributed memory system, the PaScal_TCS decomposes the computational domain into a cubic-subdomain. The numerical
procedure is based on the monolithic projection method with staggered time discretization (MPM-STD), which is 
an implicit and non-iterative solver for wall-bounded turbulent flows. 
The PaScaL_TCS has the following features.

 1. Temperature-dependent fluid properties considering non-Oberbeck–Boussinesq effect
 2. Three-dimensional domain decompositions to exploit more parallelism
 3. PaScaL_TDMA library to solve the batched tri-diagonal systems partitioned by the domain decomposition. 
 4. Two transpose schemes in parallel fast Fourier transform (FFT) for the pressure Poisson equation solver.
 5. An explicit intermediate aggregation scheme for MPI-IO is implemented to mitigate the IO burden with a massive number of cores.

# Build
```make``` command at PaScaL_TCS root directory builds a PaScaL_TCS executable binary file, 
```shell
make                       # build a PaScaL_TCS executable file
```
It also builds a PaScaL_TDMA library using ```PaScaL_TDMA/make``` and links the library to the PaScaL_TCS executable binary ```PaScaL_TCS.ex``` using a makefile in the ```src/make``` directory.
It copies the ```PaScaL_TCS.ex ``` execution file into the ```run``` directory .

# Example test
The example case is executed with the input file ```PARA_INPUT.dat``` in the ```run``` directory .
```shell
mpirun -np 8 ./PaScaL_TCS.ex 
```

The example ```PARA_INPUT.dat``` file contains the information for NOB natural convection simulation of $\Delta=10$ with $Pr=1$ at $Ra=100$ in $512\times128\times256$ meshes using 8 MPI processes. It will make ```run/data/1_continue/``` and binary outputs as follows:
```shell
cont_time.bin               # Current dimensionless time for file write and dt
cont_U.bin                  # Velocity field in x-direction for file write
cont_V.bin                  # Velocity field in y-direction for file write
cont_W.bin                  # Velocity field in z-direction for file write
cont_P.bin                  # Pressure field for file write
cont_THETA.bin              # Temperature field for file write
```

# Authors
- Ki-Ha Kim (k-kiha@yonsei.ac.kr), Multi-Physics Modeling and Computation Lab., Yonsei University
- Ji-Hoon Kang (jhkang@kisti.re.kr), Korea Institute of Science and Technology Information
- Xiaomin Pan (sanhepanxiaomin@gmail.com), Department of Mathematics, Shanghai University
- Jung-Il Choi (jic@yonsei.ac.kr), Multi-Physics Modeling and Computation Lab., Yonsei University

# Cite
Please use the following BibTeX when you refer to this project.

    @misc{PaScaL_TCS2022,
        title  = "Parallel and Scalable Library for Turbulent Convection Solver",
        author = "Kim, Ki-Ha and Kang, Ji-Hoon and Choi, Jung-Il",
        url    = "https://github.com/MPMC-Lab/PaScaL_TCS",
        year   = "2022"
    }


# References
For more information, please see the reference paper and [Multi-Physics Modeling and Computation Lab.](https://mpmc.yonsei.ac.kr/)
