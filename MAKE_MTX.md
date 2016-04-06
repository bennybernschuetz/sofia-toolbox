# SOFiA make visualisation matrix #

This function generates a matrix dataset of 1° resolution for the visualization of the array response using [visual3D](VISUAL_3D.md). It does a plane wave decomposition for 65160 directions (181ELx360AZ) using [P/D/C](PDC.md).
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/MAKEMTX_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> N           </td><td> int         </td><td> Plane wave decomposition order </td><td> 3              </td></tr>
<tr><td> Pnm         </td><td> complex float mtx </td><td> Spatial Fourier Coefficients from <a href='STC.md'>S/T/C</a> </td><td> --             </td></tr>
<tr><td> dn          </td><td> complex float mtx </td><td> Modal radial filters from <a href='MF.md'>M/F</a> </td><td> --             </td></tr>
<tr><td> krindex     </td><td> int         </td><td> index of kr-value to be visualized </td><td> 1              </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> mtxData     </td><td> float mtx   </td><td> SOFiA 3D-matrix-data </td></tr></tbody></table>

<h2>DEPENDENCIES</h2>
<a href='PDC.md'>SOFiA P/D/C</a>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_makeMTX.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
 mtxData = sofia_makeMtx(N, Pnm, dn, krIndex) <br>
 -----------------------------------------------------------------------     <br>
 mtxData   SOFiA 3D-matrix-data in 1° steps<br>
 -----------------------------------------------------------------------              <br>
 N         Order of the spatial fourier transform     [default = 3]<br>
 Pnm       Spatial Fourier Coefficients (from S/T/C)<br>
 dn        Modal Radial Filters (from M/F)<br>
 krindex   Index of kr Vector                         [default = 1]<br>
<br>
 Dependencies: SOFiA P/D/C<br>
 <br>
 The file generates a SOFiA mtxData Matrix of 181x360 pixels for the<br>
 visualisation with sofia_visual3d() in 1° Steps (65160 plane waves).<br>
<br>
*/<br>
</code></pre>