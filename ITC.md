# SOFiA Inverse Spatial Transform Core #

SOFiA S/T/C is a Inverse Spatial Fourier Transform (ISFT) core optimized for sound field analysis.
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/ITC_CORE.png' />
<br>
<br>
<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> Pnm         </td><td> complex float mtx  </td><td> Spatial Fourier coefficients </td><td> --             </td></tr>
<tr><td> angles      </td><td> float mtx   </td><td> Target angles:<br>AZ<sub>1</sub> EL<sub>1</sub>; AZ<sub>2</sub> EL<sub>2</sub>; ...; AZ<sub>M</sub> EL<sub>M</sub> for M Positions. <br>Refer to <a href='COORDINATES.md'>Coordinate System</a> </td><td> --             </td></tr>
<tr><td> <i>N</i>    </td><td> int         </td><td> Maximum transform order </td><td> Maximum available in Pnm </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> p           </td><td> complex float mtx  </td><td> Frequency domain data (pressures)</td></tr></tbody></table>


<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_itc.m </td><td> Help header </td><td> All OS    </td></tr>
<tr><td> sofia_itc.mexmaci64 </td><td> MEX core </td><td> OS-X Intel </td></tr>
<tr><td> sofia_itc.mexw32 </td><td> MEX core </td><td> Windows, MATLAB32 </td></tr>
<tr><td> sofia_itc.mexw64 </td><td> MEX core </td><td> Windows, MATLAB64 </td></tr>
<tr><td> sofia_itc.cpp </td><td> C/C++ source </td><td> All OS    </td></tr></tbody></table>

<h2>PERFORMANCE</h2>

Refer to <a href='STC.md'>S/T/C</a>.<br>
<br>
<h2>HEADER</h2>

<pre><code>/*<br>
p = ASAR_ITC(Pnm, angles, [N])<br>
------------------------------------------------------------------------<br>
p       sound pressures (complex data)  <br>
        Columns : angles<br>
        Rows    : FFT bins   <br>
------------------------------------------------------------------------<br>
Pnm     spatial Fourier coefficients (e.g. from SOFiA S/T/C)<br>
        Columns : nm coeff<br>
        Rows    : FFT bins   <br>
<br>
angles  target angles [AZ1 EL1; AZ2 EL2; ... AZn ELn]<br>
        Columns : Angle Number 1...n<br>
        Rows    : AZ EL    <br>
         <br>
[N]     *** Optional: Maximum transform order <br>
            If not specified the highest order available included in<br>
            the Pnm coefficients will be taken.<br>
<br>
This is a pure ISFT core that does not involve extrapolation. <br>
(=The pressures are refered to the original radius<br>
*/<br>
</code></pre>

The I/T/C core involves Legendre polynomials/spherical harmonics provided by the peer-reviewed <a href='http://www.boost.org'>BOOST C++ Math Library</a> under the <a href='http://www.boost.org/LICENSE_1_0.txt'>BOOST Software License</a>.