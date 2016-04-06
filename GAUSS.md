# SOFiA Gauss-Legendre Quadrature Grids #

This function computes Gauss-Legendre quadrature nodes and weigths
in the SOFiA/VariSphear data format.
<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/GAUSS_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> AZnodes     </td><td> int         </td><td> Number of azimutal nodes </td><td>  10            </td></tr>
<tr><td> ELnodes     </td><td> int         </td><td> Number of elevation nodes </td><td>  5             </td></tr>
<tr><td> <i>plot</i> </td><td> int         </td><td> Show globe plot of the grid <br> 0: Plot off, 1: Plot on </td><td>  1             </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> gridData    </td><td> float mtx   </td><td> Quadrature grid, positions and weights (W):<br>AZ<sub>1</sub> EL<sub>1</sub> W<sub>1</sub><br> AZ<sub>2</sub> EL<sub>2</sub> W<sub>2</sub><br>...<br> AZ<sub>M</sub> EL<sub>M</sub> W<sub>M</sub> for M Positions </td></tr>
<tr><td> Npoints     </td><td> int         </td><td> Number of sampling points </td></tr>
<tr><td> Nmax        </td><td> int         </td><td> Maximum Grid Order </td></tr></tbody></table>

Angles AZ, EL are in RAD. <br><br>

<h2>EXAMPLE</h2>

<img src='http://img.sofia-toolbox.googlecode.com/git/gaussexp.png' />
<br>
Gauss 10AZ/5EL Quadrature<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_gauss.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>

<h2>SOURCE OF THE QUADRATURE</h2>

Written by: Greg von Winckel - 04/13/2006<br>
<br>
<br>
<h2>HEADER</h2>
<pre><code>/*<br>
  [gridData, Npoints, Nmax] = sofia_gauss(AZnodes, ELnodes, plot)<br>
------------------------------------------------------------------------<br>
  gridData           Gauss-Legendre quadrature including weigths(W):<br>
                     [AZ_1 EL_1 W_1;<br>
                      AZ_2 EL_2 W_2;<br>
                      ...<br>
                      AZ_n EL_n W_n]<br>
 <br>
  Npoints            Total number of nodes<br>
  Nmax               Highest stable grid order  <br>
------------------------------------------------------------------------<br>
  AZnodes            Number of azimutal nodes  [default = 10]<br>
  ELnodes            Number of elevation nodes [default = 5]<br>
  plot               Show a globe plot of the selected grid <br>
                     0: Off, 1: On [default]<br>
*/<br>
</code></pre>