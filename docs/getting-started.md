## Installation

### Fortran Compiler

When starting to use **Xcompact3d** on your local workstation, it is recommended to install **gfortran** and **openmpi** (preferably with an **Ubuntu** distribution). It is possible to download the latest archive for **openmpi** from the address [www.open-mpi.org/software/ompi/v3.1/](https://www.open-mpi.org/software/ompi/v3.1/). See below for the installation of **gfortran** and **openmpi**:
``` Bash
sudo apt-get install build-essential
sudo apt-get install gfortran
tar -xvzf openmpi-***.tar.gz
cd openmpi***
sudo ./configure  --prefix=/usr/local F77=gfortran FC=gfortran
sudo make all install
```
It is also necessary to add a line in the `.bashrc` file:
``` Bash
export LD_LIBRARY_PATH=/usr/local/lib/
```

### Downloading the code

Download the last release directly from the [repository](https://github.com/xcompact3d/Incompact3d/releases) or acquire the source code by cloning the git repository:

``` Bash
git clone git@github.com:xcompact3d/Incompact3d.git
```

???+ note "If you are behind a firewall"
    You may need to use the `https` protocol instead of the `git` protocol:

    ``` Bash
    git config --global url."https://".insteadOf git@
    ```

    Be sure to also configure your system to use the appropriate proxy settings, e.g. by setting the `https_proxy` and `http_proxy` variables.

By default you will be building the latest master version of Xcompact3d, to use the release preview you must checkout the release branch

``` Bash
git checkout release
```

### Updating an existing source tree

If you have previously downloaded `incompact3d` using `git clone`, you can update the existing source tree using `git pull` rather than starting anew:

``` Bash
cd incompact3d
git pull && make
```

Assuming that you had made no changes to the source tree that will conflict with upstream updates, these commands will trigger a build to update to the latest version.

### Known issues

Some users have experienced difficulties with the MPI librairy `mpich`.  Other than that **Xcompact3d** has been used on a wide range of supercomputers with various compilers and MPI librairies.

It is strongly recommended to carefully read the documentation of the supercomputer you will be using. You should be able to find all the information you need about the optimum compiler options.

## Compiling Incompact3d

Now run `make` to build the `Xcompact3d` executable.
This takes a while, but only has to be done once. If the defaults in the build do not work for you, and you need to set specific make parameters, you can save them in `Make.user`. The build will automatically check for the existence of `Makefile` and use it if it exists. Building Xcompact3d requires very little of disk space and virtual memory.

The command `make post` compiles the new post-processing utility. To remove all binary files type `make clean`, it is also recommended when any compilation flag or variables defined in Fortran as parameters are changed. `make cleanall` is more aggressive, it removes all binaries besides all files produced during simulation.

## Input Files

The name of each variable is clearly explained in the `input.i3d` file. All quantities are non-dimentionalised with a length and a velocity.

The domain size is \( xlx \times yly \times zlz \) and it is discritised in \( nx \times ny \times nz \) mesh points. Notice that the number of mesh points in a direction \( i \) should respect the following equation:

$$
n_i = \left\{ \begin{array}{ll} 2^{1+a} \times 3^b \times 5^c &\mbox{if periodic,} \\ 2^{1+a} \times 3^b \times 5^c + 1 &\mbox{otherwise,}
\end{array} \right.
$$

where $a$, $b$ and $c$ are integers.

???+ example "Examples for non-periodic case"
    7 9 11 13 17 19 21 25 31 33 37 41 49 51 55 61 65 73 81 91 97 101 109 121 129 145 151 161 163 181 193 201 217 241 251 257 271 289 301 321 325 361 385 401 433 451 481 487 501 513 541 577 601 641 649 721 751 769 801 811 865 901 961 973 1001 1025 1081 1153 1201 1251 1281 1297 1351 1441 1459 1501 1537 1601 1621 1729 1801 1921 1945 2001 2049 2161 2251 2305 2401 2431 2501 2561 2593 2701 2881 2917 3001 3073 3201 3241 3457 3601 3751 3841 3889 4001 4051 4097 4321 4375 4501 4609 4801 4861 5001 5121 5185 5401 5761 5833 6001 6145 6251 6401 6481 6751 6913 7201 7291 7501 7681 7777 8001 8101 8193 8641 8749 9001 9217 9601...

    For periodic cases, just subtract one.


There is no check on the time step `dt`, so it is your responsability to carefully investigate about the stability conditions for your simulation. The optimum time step has to be defined with a trial-and-error procedure.

The time step is fixed for a given simulation. It is not possible (yet?) to use a different time step at each time step.

The parameters `p_row` and `p_col` are associate with the 2D Pencil Decomposition (see [2DECOMP&FFT](http://www.2decomp.org/)) for large-scale parallel applications. Notice that the product of both should be equal to the number of computational cores where Xcompact3d will run.

!!! tip
    Setting `p_row = p_col = 0` activates the auto-tuning mode, where the code chooses the fastest combination.

More details are available in six exemplified flow configuration:

  * [Periodic Channel Flow](./Flow-Configurations/channel-flow.md)
  * [Flow Over a Cylinder](./Flow-Configurations/cylinder.md)
  * [Gravity Current (Lock-Exchange)](./Flow-Configurations/lock-exchange.md)
  * [Mixing Layer](./Flow-Configurations/mixing-layer.md)
  * [Taylor-Green Vortices](./Flow-Configurations/taylor-green-vortex.md)
  * [Turbulent Boundary Layer](./Flow-Configurations/turbulent-boundary-layer.md)

## Running the code

Now you should be able to run Xcompacted3d like this:

``` Bash
mpirun -n <number of cores> ./xcompact3d ./examples/<EXAMPLE>/input.i3d
```

If a `input.i3d` file is not provided, Xcompact3d will look for it locally (i.e. try to load ./input.i3d)

!!! tip
    It is a good practice to save the execution log into a file, in Linux, for instance, it can be done using the command:

    ```
      mpirun -n <number of cores> ./xcompact3d ./examples/<EXAMPLE>/input.i3d > log.out
    ```
