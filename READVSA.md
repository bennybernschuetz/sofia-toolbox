# VariSphear dataset import #

The function `readVSAdata()` imports array data from a VariSphear system. The function parses the VariSphear data to structs that can be read by the [SOFiA F/D/T](FDT.md) frequency domain transform.<br><br>
The <code>readVSAdata()</code> function allows to downsample and normalize the impulse responses. It calculates the average air temperature and delivers the quadrature grid positions and weights. If no directory is given a user dialog will open to pick a directory.<br>
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/READVSA_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>
<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> <i>downSample</i> </td><td> int         </td><td> Downsample Factor </td><td> 1              </td></tr>
<tr><td> <i>normalize</i> </td><td> int         </td><td> Normalization Flag 1:on 0:off </td><td> 1              </td></tr>
<tr><td> <i>directory</i> </td><td> string      </td><td> VSA Session Directory </td><td> uigetdir()     </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> timeDataCH1 </td><td> struct      </td><td> Time domain Data for CH1 </td><td> -              </td></tr>
<tr><td> timeDataCH2 </td><td> struct      </td><td> Time domain Data for CH2 </td><td> -              </td></tr></tbody></table>

The structs contain the following fields:<br>
<br>
<table><thead><th> <b>Field</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> .impulseResponses </td><td> float mtx   </td><td> Impulse Response Data N:Channels, M:Samples </td></tr>
<tr><td> .FS          </td><td> int         </td><td> Sampling Frequency  </td></tr>
<tr><td> .quadratureGrid  </td><td> float mtx   </td><td> Quadrature Grid Data AZ1 EL1 W1; ...; AZn ELn Wn  </td></tr>
<tr><td> .metaData    </td><td> cell array  </td><td> VSD structs from VariSphear session </td></tr>
<tr><td> .downSample  </td><td> int         </td><td> Downsampling Factor (from Input)  </td></tr>
<tr><td> .averageAirTemp  </td><td> float       </td><td> Average air temperature of the session (default 20°C if not captured) </td></tr>
<tr><td> .irOverlay   </td><td> float vector </td><td> Overlay of all impulse responses (PLOT) </td></tr></tbody></table>

The content of <code>timeDataCH1</code> and <code>timeDataCH1</code> depends on the VariSphear session type:<br>
<br>
<table><thead><th> <b>Session Type</b> </th><th> <b>Microphones</b> </th><th> <b>timeDataCH1</b> </th><th> <b>timeDataCH2</b> </th></thead><tbody>
<tr><td> Single Sphere       </td><td> 1                  </td><td> full dataset       </td><td> empty              </td></tr>
<tr><td> Half Sphere         </td><td> 2                  </td><td> full dataset       </td><td> empty              </td></tr>
<tr><td> Dual Sphere         </td><td> 2                  </td><td> Radius 1 dataset (CH1) </td><td> Radius 2 dataset (CH2) </td></tr></tbody></table>

<br>

<h2>SOME DETAILS</h2>
The downsampling is done using DECIMATE and a FIR low pass filter of order 30. See MATLAB documentation for more information.<br> <b>(MATLAB Signal Processing Library required for downsampling.)</b><br><br>
The normalization is done with respect to the highest overall value found in the complete session.<br>
<br>
<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_readVSAdata.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
[timeDataCH1, timeDataCH2] = readVSA_data([downSample], [normalize], [directory])<br>
------------------------------------------------------------------------     <br>
timeData            Struct with fields:<br>
<br>
                    .impulseResponses     [Channels x Samples]          <br>
                    .FS<br>
                    .quadratureGrid       [AZ1 EL1 W1; ...; AZn ELn Wn]<br>
                    .metaData             Cell Array, VSA Metadata<br>
                    .downSample<br>
                    .averageAirTemp       Temperature in °C <br>
                    .irOverlay            Plot this for a good total <br>
                                          overview of the dataset.<br>
------------------------------------------------------------------------              <br>
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
*/<br>
</code></pre>