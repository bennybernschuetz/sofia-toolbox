# SOFiA Lebedev Quadrature Grids #

This function computes Lebedev quadrature nodes and weigths
in the SOFiA/VariSphear data format.
<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/LEBEDEV_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> Degree      </td><td> int         </td><td> Degree/Number of points  <br><br> Valid Degrees are:<br> 6, 14, 26, 38, 50, 74, 86, 110, 146, 170, <br>194, 230, 266, 302, 350, 434, 590, 770, <br>974, 1202, 1454, 1730, 2030, 2354, 2702, <br> 3074, 3470, 3890, 4334, 4802, 5294, 5810<br><br> Call: sofia_lebedev() to obtain valid degrees</td><td>  --            </td></tr>
<tr><td> <i>plot</i> </td><td> int         </td><td> Show globe plot of the grid <br> 0: Plot off, 1: Plot on </td><td>  1             </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> gridData    </td><td> float mtx   </td><td> Quadrature grid, positions and weights (W):<br>AZ<sub>1</sub> EL<sub>1</sub> W<sub>1</sub><br> AZ<sub>2</sub> EL<sub>2</sub> W<sub>2</sub><br>...<br> AZ<sub>M</sub> EL<sub>M</sub> W<sub>M</sub> for M Positions </td></tr>
<tr><td> Npoints     </td><td> int         </td><td> Number of sampling points </td></tr>
<tr><td> Nmax        </td><td> int         </td><td> Maximum Grid Order </td></tr></tbody></table>

Angles AZ, EL are in RAD. <br><br>

<h2>EXAMPLE</h2>

<img src='http://img.sofia-toolbox.googlecode.com/git/lebedevexp.png' />
<br>
Lebedev 50P Quadrature<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_lebedev.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>

<h2>SOURCE OF THE QUADRATURE</h2>

author Rob Parrish, The Sherrill Group, CCMST Georgia Tech<br>
date 03/24/2010<br>


<h2>HEADER</h2>
<pre><code>/*<br>
[gridData, Npoints, Nmax] = sofia_lebedev(degree, plot)<br>
------------------------------------------------------------------------<br>
<br>
  gridData           Lebedev quadrature including weigths(W):<br>
                     [AZ_1 EL_1 W_1;<br>
                      AZ_2 EL_2 W_2;<br>
                      ...<br>
                      AZ_n EL_n W_n]<br>
 <br>
  Npoints            Total number of nodes<br>
  Nmax               Highest stable grid order  <br>
------------------------------------------------------------------------<br>
  Order              Lebedev Degree (Number of nodes)<br>
                     Call sofia_lebedev() to obtain a <br>
                     list of valid degrees.<br>
 <br>
  plot               Show a globe plot of the selected grid <br>
                     0: Off, 1: On [default]<br>
*/<br>
</code></pre>