# Import array dataset #
The function mergeArrayData() merges array measurement data to structs that can be read by the SOFiA F/D/T frequency domain transform. The mergeArrayData() function allows to downsample and normalize the impulse responses.
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/MERGEARRAY_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>
<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> impulseResponses </td><td> float mtx   </td><td> Impulse Response Data<br>Rows: IR-Data<br>Cols: Different positions </td><td> --             </td></tr>
<tr><td> FS          </td><td> int         </td><td> Sampling Frequency </td><td> --             </td></tr>
<tr><td> <i>temperature</i> </td><td> float       </td><td> Air Temperature in °C </td><td> 20             </td></tr>
<tr><td> <i>downSample</i> </td><td> int         </td><td> Downsample Factor </td><td> 1              </td></tr>
<tr><td> <i>normalize</i> </td><td> int         </td><td> Normalization Flag 1:on 0:off </td><td> 1              </td></tr></tbody></table>


<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> timeData    </td><td> struct      </td><td> Time domain Data </td><td> -              </td></tr></tbody></table>


The struct contains fields:<br>
<br>
<table><thead><th> <b>Field</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> .impulseResponses </td><td> float mtx   </td><td> Impulse Response Data N:Channels, M:Samples </td></tr>
<tr><td> .FS          </td><td> int         </td><td> Sampling Frequency  </td></tr>
<tr><td> .downSample  </td><td> int         </td><td> Downsampling Factor (from Input)  </td></tr>
<tr><td> .averageAirTemp  </td><td> float       </td><td> Average air temperature  </td></tr>
<tr><td> .irOverlay   </td><td> float vector </td><td> Overlay of all impulse responses (PLOT) </td></tr></tbody></table>


<h2>SOME DETAILS</h2>
The downsampling is done using DECIMATE and a FIR low pass filter of order 30. See MATLAB documentation for more information.<br> <b>(MATLAB Signal Processing Library required for downsampling.)</b><br><br>
The normalization is done with respect to the highest overall value found in the complete session.<br>
<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_mergeArrayData.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
timeData = sofia_mergeArrayData(impulseResponses, FS, temperature,...<br>
                                             [downSample], [normalize])<br>
------------------------------------------------------------------------     <br>
timeData            Struct with fields:<br>
<br>
                    .impulseResponses     [N:Channels M:Samples]          <br>
                    .FS<br>
                    .downSample<br>
                    .averageAirTemp       Temperature in DEG <br>
                    .irOverlay            Plot this for a good total <br>
                                          overview of the dataset.<br>
------------------------------------------------------------------------<br>
impulseResponses   Impulse response data [M:Channels N:Samples]<br>
                   !The audio data must be in in columns as it is  <br>
                   usual in MATLAB. But SOFiA works on audio data <br>
                   in rows as it is usual in audio editors etc.<br>
                   Therefore the output IR matrix is flipped over.<br>
<br>
                   WARNING: Be sure the IRs come in the same order  <br>
                   as the sample grid points are organized!<br>
<br>
FS                 Sampling frequency of the source material in 1/s<br>
<br>
radius             Array sphere radius in meters<br>
<br>
temperature        Average air temperature during the capture<br>
                   This is important for F/D/T to calculate the<br>
                   kr-vector. (This value is simply passed thru).<br>
<br>
downSample         Downsampling factor  [default = 1: No downsampling]<br>
                   Downsampling is done using DECIMATE and a FIR low <br>
                   pass filter of order 30. See MATLAB documentation <br>
                   for more information. <br>
                   !!! MATLAB Signal Processing Library required<br>
<br>
normalize          Normalize flag 1:on, 0:off         [default = 1: on]       <br>
                   Normalizes the impulse responses with respect to the <br>
                   absolute maximum value within the complete dataset.<br>
<br>
directory          VSA dataset directory. If not defined a user dialog<br>
                   opens to pick a directory.<br>
<br>
<br>
*/<br>
</code></pre>