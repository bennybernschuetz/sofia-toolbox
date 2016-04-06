# SOFiA Plane Wave Decomposition Core #

SOFiA P/D/C is a plane wave decomposition and beamforming core. P/D/C can deliver plane wave outputs for a whole vector of angles (array look directions) at the same time. The core natively does a plane wave decomposition but can be switched to a beamformer using the c<sub>n</sub> coefficients. The c<sub>n</sub> coefficients can be defined as a vector n=0...N  for constant directivity beamforming or as a matrix for frequency-dependent beamshaping. The decomposer is normalized, a plane wave of unity magnitude will always deliver an output of 0dB in look direction.
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/PDC_CORE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> N           </td><td> int         </td><td> Maximum decomposition order </td><td> --             </td></tr>
<tr><td> OmegaL      </td><td> float mtx   </td><td> Array look direction (AZ1 EL1; AZ2 EL2;... ; AZn ELn) in RAD <br>Refer to <a href='COORDINATES.md'>Coordinate System</a> </td><td> --             </td></tr>
<tr><td> Pnm         </td><td> complex float mtx </td><td> Spatial Fourier coefficiens from <a href='STC.md'>S/T/C</a> </td><td> --             </td></tr>
<tr><td> dn          </td><td> complex float mtx </td><td> Radial Filter coefficients from <a href='MF.md'>M/F</a>  </td><td> --             </td></tr>
<tr><td> <i>cn</i>   </td><td> complex float vec or mtx </td><td> Optional: Beamshaping coefficients (CD or kr-dependent) </td><td> --             </td></tr></tbody></table>


<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> Y           </td><td> complex float mtx  </td><td> Spectral FFT data </td></tr></tbody></table>


<h2>DEFINITIONS</h2>

<img src='http://img.sofia-toolbox.googlecode.com/git/PWD_FORMULA.png' />

Where Y<sub>nm</sub> describes the <a href='http://mathworld.wolfram.com/SphericalHarmonic.html'>Spherical Harmonics</a> of order n and modus m.<br>
<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_pdc.m </td><td> Help header </td><td> All OS    </td></tr>
<tr><td> sofia_pdc.mexmaci64 </td><td> MEX core </td><td> OS-X Intel </td></tr>
<tr><td> sofia_pdc.mexw32 </td><td> MEX core </td><td> Windows, MATLAB32 </td></tr>
<tr><td> sofia_pdc.mexw64 </td><td> MEX core </td><td> Windows, MATLAB64 </td></tr>
<tr><td> sofia_pdc.cpp </td><td> C/C++ source </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
Y = sofia_pdc(N, OmegaL, Pnm, dn, [cn]) <br>
------------------------------------------------------------------------     <br>
Y       MxN Matrix of the decomposed wavefield <br>
        Col - Look Direction as specified in OmegaL<br>
        Row - kr bins<br>
------------------------------------------------------------------------              <br>
N       Decomposition Order<br>
<br>
OmegaL  Look Directions (Vector) <br>
        Col - L1, L2, ..., Ln <br>
        Row - AZn ELn<br>
<br>
Pnm     Spatial Fourier Coefficients from SOFiA S/T/C<br>
<br>
dn      Modal Array Filters from SOFiA M/F<br>
<br>
cn      (Optional) Weighting Function<br>
        Can be used for N=0...N weigths:<br>
        Col - n...N<br>
        Row - 1<br>
        Or n(f)...N(f) weigths:<br>
        Col - n...N<br>
        Row - kr bins   <br>
        If cn is not specified a PWD will be done<br>
*/<br>
<br>
</code></pre>

The P/D/C core involves Legendre polynomials/spherical harmonics provided by the peer-reviewed <a href='http://www.boost.org'>BOOST C++ Math Library</a> under the <a href='http://www.boost.org/LICENSE_1_0.txt'>BOOST Software License</a>.