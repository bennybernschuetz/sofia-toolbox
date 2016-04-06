# SOFiA Radial Filter Improvement #

This function improves the FIR radial filters from SOFiA M/F. The filters are made causal and are windowed in time domain. The DC components are estimated. The R/F/I module should always be inserted to the filter path when treating measured data even if no use is made of the included kernel downscaling or highpass filters.
<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/RFI_NATIVE.png' />
<br>
<br>

<h3>INFORMATION</h3>

If HPF is on (highPass>0) the radial filter kernel is<br>
downscaled by a factor of two. Radial Filters and HPF share the available taps and the latency keeps constant. Be careful using very small signal blocks because there may remain too few taps. Observe the filters by plotting their spectra and impulse responses. <br>
<ul><li>Be very carefull if NFFT/max(kr) < 25 (Low spectral density)<br>
</li><li>Do not use R/F/I if NFFT/max(kr) < 15 (Very low spectral density)<br>
</li><li>Do NOT use R/F/I for single open sphere filters (e.g.simulations). <br><br></li></ul>

<h3>IMPORTANT</h3>

Remember to choose a fft-oversize factor (F/D/T) large enough to cover all filter latencies and reponse slopes.  Otherwise undesired cyclic convolution artifacts may appear in the output signal.<br>
<br>
<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> dn          </td><td> complex float mtx </td><td>  Analytical frequency domain radial filter coeficients from M/F </td><td> --             </td></tr>
<tr><td> <i>kernelDownscale</i> </td><td> int         </td><td> Downscale filer kernel in powers of 2 </td><td> 2              </td></tr>
<tr><td> <i>highPass</i> </td><td> float       </td><td> Highpass Filter 0:highPass:1,<br>             highPass = 1 corresponds to the max kr available.<br>               highPass = 0 filter off (#default)  </td><td> 0              </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> dn          </td><td> complex float mtx </td><td> Improved frequency domain radial filter coeficients</td></tr>
<tr><td> kernelSize  </td><td> int         </td><td> current total size of the filter kernel (in samples) </td></tr>
<tr><td> latency     </td><td> int         </td><td> approximated latency due to the filters (in samples) </td></tr></tbody></table>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_rfi.m </td><td> Help header, Function </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
 function [dn, kernelSize, latency] =  <br>
                    sofia_rfi(dn, kernelDownScale, highPass)<br>
 ------------------------------------------------------------------------     <br>
 dn                 Improved radial filters<br>
 kernelSize         Filter kernel size (total)<br>
 latency            Approximate signal latency due to the filters<br>
         <br>
 ------------------------------------------------------------------------              <br>
 dn                 Analytical frequency domain radial filters <br>
                    from SOFiA M/F<br>
 kernelDownScale    Downscale factor for the filter kernel #default: 2                                   <br>
 highPass           Highpass Filter 0:highPass:1<br>
                    highPass = 1 corresponds to the max kr available.<br>
                    highPass = 0 filter off (#default) <br>
<br>
*/<br>
</code></pre>