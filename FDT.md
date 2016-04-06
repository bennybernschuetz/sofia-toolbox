# SOFiA frequency domain transform #

F/D/T transforms the time domain array data into spectral frequency domain data using the [Fast Fourier Transform (FFT)](http://www.mathworks.com/help/techdoc/math/brentm1-1.html). As a default setting the full length impulse responses are tranformed with a Blocksize `NNFT=2^(nextpow2(length_of_impulseresponses))`. The blocksize can be rised by using FFToversize which is a multiplier of NFFT (Default = 2). A limited time section can be picked out by defining `firstSample` and `lastSample`. The length of this section is `(lastSample-firstSample)`. This way unnecessary data can be removed or a running window can be realized to obtain time slices and resolve the temporal information within the captured sound field.
<br><br>
To save processing power and calculation time the SOFiA chain works on the half-sided FFT spectrum only (NFFT/2+1). Therefore F/D/T produces  half-sided spectrum output signals (fftData). Later the <a href='MAKE_IR.md'>makeIR</a> function automatically reconstructs the double-sided spectrum to compute impulse responses.<br>
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/FDT_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>
<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> timeData    </td><td> struct      </td><td> Time domain data from <a href='READ_VSA.md'>sofia_readVSAdata()</a> or <a href='MERGE_DATA.md'>sofia_mergeArrayData()</a> </td><td> --             </td></tr>
<tr><td> <i>FFToversize</i> </td><td> int         </td><td> Rises the FFT Blocksize </td><td> 2              </td></tr>
<tr><td> <i>firstSample</i> </td><td> int         </td><td> Start sample in time domain data </td><td> 1              </td></tr>
<tr><td> <i>lastSample</i> </td><td> int         </td><td> End sample in time domain data </td><td> length of timeData.impulseReponses</td></tr></tbody></table>

The struct timeData contains minimum fields:<br>
<br>
<table><thead><th> <b>Field</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> .impulseResponses </td><td> float mtx   </td><td> Impulse Response Data N:Channels, M:Samples </td></tr>
<tr><td> .FS          </td><td> int         </td><td> Sampling Frequency  </td></tr>
<tr><td> .downSample  </td><td> int         </td><td> Downsampling Factor (from Input)  </td></tr>
<tr><td> .averageAirTemp  </td><td> float       </td><td> Average air temperature  </td></tr></tbody></table>


<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> fftData     </td><td> complex float mtx </td><td> Frequency domain data for <a href='STC.md'>S/T/C</a></td></tr>
<tr><td> kr          </td><td> float vec   </td><td> kr Values (k: wave number, r: radius) </td></tr>
<tr><td> f           </td><td> float vec   </td><td> Absolute frequency scale </td></tr></tbody></table>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_fdt.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
[fftData, kr, f] = sofia_fdtVSA(timeData, FFToversize, <br>
                                  firstSample, lastSample)<br>
------------------------------------------------------------------------<br>
fftData           Frequency domain data ready for the Spatial <br>
                  Fourier Transform (SOFiA S/T/C Core)<br>
                  ! To save processing power the SOFiA chain always<br>
                    works on the half-sided FFT spectrum only (NFFT/2+1)<br>
kr                kr-Values of the delivered data (required e.g. for the <br>
                  modal radial filters SOFiA M/F)<br>
f                 Absolute frequency scale. Not really required but good <br>
                  for control purposes or scaling a spectrum plot.<br>
------------------------------------------------------------------------ <br>
timeData          Struct with minimum fields: <br>
<br>
                  * .impulseResponses     [Channels X Samples]          <br>
                  * .FS<br>
                  * .radius               Array radius<br>
                  * .averageAirTemp       Temperature in DEG <br>
<br>
<br>
FFToversize       FFToversize rises the FFT Blocksize.   [default = 2] <br>
                  A FFT of the blocksize (FFToversize*NFFT) is applied <br>
                  to the time domain data,  where  NFFT is determinded  <br>
                  as the next power of two of the signalSize  which is<br>
                  signalSize = (lastSample-firstSample).                   <br>
<br>
                  The function will pick a window of <br>
                  (lastSample-firstSample) for the FFT:<br>
<br>
firstSample       First time domain sample to be included <br>
lastSample        Last time domain sample to be included<br>
                  If firstSample and lastSample are not defined <br>
                  the full IR will be transformed:<br>
                  [ default: firstSample = 1;<br>
                    lastSample = size(timeData.impulseResponses,2);]<br>
<br>
Call this function with a running window (firstSample+td-&gt;lastSample+td) <br>
increasing td to obtain time slices. This way you resolve the<br>
temporal information within the captured sound field.                  <br>
*/<br>
</code></pre>