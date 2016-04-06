# SOFiA Spatial Transform Core #

SOFiA S/T/C is a Spatial Fourier Transform (SFT) core optimized for sound field analysis.
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/STC_CORE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> N           </td><td> int         </td><td> Maximum transform order </td><td> --             </td></tr>
<tr><td> fftData     </td><td> complex float mtx  </td><td> Frequency domain data e.g. from <a href='FDT.md'>F/D/T</a> </td><td> --             </td></tr>
<tr><td> grid        </td><td> float mtx   </td><td> Quadrature grid, positions and weights:<br>AZ<sub>1</sub> EL<sub>1</sub> W<sub>1</sub>; AZ<sub>2</sub> EL<sub>2</sub> W<sub>2</sub>; ...; AZ<sub>M</sub> EL<sub>M</sub> W<sub>M</sub> for M Positions. <br>Refer to <a href='COORDINATES.md'>Coordinate System</a> </td><td> --             </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> Pnm         </td><td> complex float mtx  </td><td> Spatial Fourier coefficients </td></tr></tbody></table>


<h2>DEFINITIONS</h2>

<img src='http://img.sofia-toolbox.googlecode.com/git/SFT_FORMULA.png' />

Where Y<sub>nm</sub> describes the <a href='http://mathworld.wolfram.com/SphericalHarmonic.html'>Spherical Harmonics</a> of order n and modus m. Beta are the grid weights and p the complex sound pressures.<br>
<br>
<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_stc.m </td><td> Help header </td><td> All OS    </td></tr>
<tr><td> sofia_stc.mexmaci64 </td><td> MEX core </td><td> OS-X Intel </td></tr>
<tr><td> sofia_stc.mexw32 </td><td> MEX core </td><td> Windows, MATLAB32 </td></tr>
<tr><td> sofia_stc.mexw64 </td><td> MEX core </td><td> Windows, MATLAB64 </td></tr>
<tr><td> sofia_stc.cpp </td><td> C/C++ source </td><td> All OS    </td></tr></tbody></table>

<h2>WARNINGS</h2>

If the S/F/T core crashes it might be necessary to typecast <code>fftData</code> to double before calling the external:<br>
<br>
<code>fftData = cast(fftData, 'double');</code>

<h2>PERFORMANCE</h2>

The SOFiA transform cores S/T/C and I/T/C offer a high computation speed and a stable and precise transform at the same time.<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/STCPERFORMANCE.png' />

Two performance examples of the S/T/C core. The <b>left plot</b> shows the runtime for transforms on different FFT blocksizes for a rising number of sensors M at a maximum order <code>N = floor(sqrt(M/2)-1)</code>. The FFT blocksize has a linear influence on the runtime. The <b>right plot</b> shows a comparison to the high performance transform algorithm of the Intel Performance Primitives (IPP). The IPP transform is made for computer graphics rendering and not optimized for sound field analysis. The IPP transform can only run up to N=15 and delivers real-valued coefficients that have to be converted to complex ones. The S/T/C core is not order-limited and runs even faster than the IPP transform for sound field analysis.<br>
<br>
<br>
<h2>HEADER</h2>
<pre><code>/*<br>
Pnm = sofia_stc(N, fftData, grid)<br>
------------------------------------------------------------------------<br>
Pnm      Spatial Fourier Coefficients <br>
         Columns : nm coeff<br>
         Rows    : FFT bins   <br>
------------------------------------------------------------------------   <br>
N        Maximum transform order<br>
<br>
fftdata  Frequency domain sounfield data, e.g. from sofia_fdt()<br>
         Columns : number of spatial sampling position <br>
         Rows    : FFT bins (complex sound pressure data)<br>
<br>
         ! WARNING cast fftdata to double if core crashes:<br>
           fftData = cast(fftData, 'double');<br>
<br>
grid     Sample grid (Positions and Weights)<br>
         Columns : s=1...S spatial sampling positions<br>
         Rows    : [AZ_s EL_s GridWeight_s]<br>
         AZ in [0...2pi] and EL [0...pi] in RAD<br>
<br>
*/<br>
</code></pre>

The S/F/T core involves Legendre polynomials/spherical harmonics provided by the peer-reviewed <a href='http://www.boost.org'>BOOST C++ Math Library</a> under the <a href='http://www.boost.org/LICENSE_1_0.txt'>BOOST Software License</a>.