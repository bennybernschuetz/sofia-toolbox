# Feature Overview #

  * Fast SFT - Spatial Fourier Transform, [S/T/C](STC.md) (CORE)
  * Fast ISFT - Inverse Spatial Fourier Transform, [I/T/C](ITC.md) (CORE)
  * Modal radial filters for spherical arrays, [M/F](MF.md) (CORE)
  * Plane wave decomposition and beamforming, [P/D/C](PDC.md) (CORE)
  * Radial filter improvement [R/F/I](RFI.md)
  * Sound field extrapolation, [S/F/E](SFE.md)
  * Wave Generators, [W/G/C](WGC.md) and [S/W/G](SWG.md)
  * 3D Visualization, [makeMTX](MAKE_MTX.md) and [visual3D](VISUAL_3D.md)
  * Directional impulse responses/time signals, [makeIR](MAKE_IR.md)
  * VariSphear dataset import, [readVSAdata](READ_VSA.md)
  * Array example datasets under Creative Commons License
  * [Gauss-Legendre](GAUSS.md) and [Lebedev](LEBEDEV.md) Quadrature Grids
<br></li></ul>

<img src='http://img.sofia-toolbox.googlecode.com/git/gpl3ccsm.jpg' />

The externals (cores) are the heart of SOFiA. Precompiled cores for MATLAB 64 Bit on MAC-OS, MATLAB 32 and 64 Bits on Windows and MATLAB 32 Bit on Linux are included in the package. (Thanx to Julian Strobl for compiling the cores on Linux 32 Bit!) The cores involve Legendre polynomials/spherical harmonics and Bessel/Hankel functions provided by the peer-reviewed <a href='http://www.boost.org'>BOOST C++ Math Library</a> under the <a href='http://www.boost.org/LICENSE_1_0.txt'>BOOST Software License</a>.