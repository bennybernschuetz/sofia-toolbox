# SOFiA Sound Field Extrapolation #

S/F/E offers basic sound field extrapolation from radius _ra_ to radius _rb_.
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/SFE_NATIVE.png' />
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> Pnm_kra     </td><td> complex float mtx  </td><td> Spatial Fourier coefficients related to radius a </td><td> --             </td></tr>
<tr><td> kra         </td><td> float vec   </td><td> Source kr-Vector with radius r=ra </td><td> --             </td></tr>
<tr><td> krb         </td><td> float vec   </td><td> Target kr-Vector with radius r=rb </td><td> --             </td></tr>
<tr><td> problem     </td><td> int         </td><td> 1: Interior problem 2: Exterior problem </td><td> 1              </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> Pnm_krb     </td><td> complex float mtx  </td><td> Spatial Fourier coefficients related to radius b </td></tr></tbody></table>

A more powerful extrapolation core is scheduled to be implemented in a future release.<br>
<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_sfe.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>

<h2>HEADER</h2>
<pre><code>/*<br>
Pnm_krb = sofia_sfe(Pnm_kra, kra, krb, problem) <br>
 ------------------------------------------------------------------------     <br>
 Pnm_krb Spatial Fourier Coefficients, extrapolated to rb<br>
 ------------------------------------------------------------------------              <br>
 <br>
 Pnm_kra Spatial Fourier Coefficients from SOFiA S/T/C<br>
 <br>
 kra     k*ra Vector<br>
 krb     k*rb Vector<br>
 problem 1: Interior problem [default]  2: Exterior problem<br>
*/<br>
</code></pre>