<a name="logo"/>
<div align="center">
<a href="https://www.incompact3d.com" target="_blank">
<img src="https://www.incompact3d.com/uploads/5/8/7/2/58724623/incompact3d.png" alt="Logo" width="300" height="100"></img>
</a>
</div>

Xcompact3d is a powerful high-order flow solver for academic research. Dedicated to Direct and Large Eddy Simulations (DNS/LES), it can combine the versatility of industrial codes with the accuracy of spectral codes. It scales with up to one million cores.
The incompressible Navier-Stokes equations are discretized with finite-difference sixth-order schemes on a Cartesian mesh. Explicit or semi-implicit temporal schemes can be used for the time advancement depending on the flow configuration. To treat the incompressibility condition, a fractional step method requires to solve a Poisson equation. This equation is fully solved in spectral space via the use of relevant 3D Fast Fourier transforms(FFTs), allowing any kind of boundary conditions for the velocity field in each spatial direction. Using the concept of the modified wavenumber, the divergence free condition is ensured up to machine accuracy. The pressure field is staggered from the velocity field by half a mesh to avoid spurious oscillations.  
The modelling of a solid body inside the computational domain is performed with a customised Immersed Boundary Method. It is based on a direct forcing to ensure a no-slip boundary condition at the wall of the solid body while imposing non-zero velocities inside the solid body to avoid discontinuities on the velocity field. This customised IBM, fully compatible with the 2D domain decomposition ([2DECOMP&FFT](http://www.2decomp.org)) and with a possible mesh refinement at the wall, is based on a 1D expansion of the velocity field from fluid regions into solid regions using Lagrange polynomials.
To reach realistic Reynolds numbers, an implicit LES strategy can be implemented to solve the Navier-Stokes equations without any extra explicit modelling. In order to mimic a subgrid-scale model, artificial dissipation can be added via the viscous term thanks to the artificial dissipative features of the high-order compact schemes.

**More information about the numerical methods can be found in:**

* Laizet, S., & Lamballais, E. (2009). High-order compact schemes for incompressible flows: A simple and efficient method with quasi-spectral accuracy. Journal of Computational Physics, 228(16), 5989-6015.

* Lamballais, E., Fortuné, V., & Laizet, S. (2011). Straightforward high-order numerical dissipation via the viscous term for direct and large eddy simulation. Journal of Computational Physics, 230(9), 3270-3275.

**More information about the parallel strategy of the code can be found in:**

* Laizet, S., & Li, N. (2011). Incompact3d: A powerful tool to tackle turbulence problems with up to O (105) computational cores. International Journal for Numerical Methods in Fluids, 67(11), 1735-1757.

* Li, N., & Laizet, S. (2010, May). 2DECOMP & FFT-a highly scalable 2d decomposition library and FFT interface. In Cray User Group 2010 conference (pp. 1-13).

* Laizet, S., Lamballais, E., & Vassilicos, J. C. (2010). A numerical strategy to combine high-order schemes, complex geometry and parallel computing for high-resolution DNS of fractal generated turbulence. Computers & Fluids, 39(3), 471-484.

**IMPORTANT:**

* **It is strongly recommended to read the previous references before starting using Xcompact3d.**

* **We kindly ask you to cite the previous references (when suitable) in your work based on Xcompact3d.**

!!! warning
    This website is still under development, some unexpected behaviors may be noticed.
