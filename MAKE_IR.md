# SOFiA impulse response reconstruction #

This function recombines impulse responses for multiple channels from
frequency domain data delivered by [P/D/C](PDC.md) or [I/T/C](ITC.md). The internal [IFFT](http://www.mathworks.com/help/techdoc/ref/ifft.html) blocklength is determined by the Y data itself: Y should have a size of `[NumberOfChannels x ((2^n)/2)+1]` with `n={1,2,3,...}` (which is the case when using the SOFiA [readVSAdata()](READ_VSA.md) or [mergeArrayData()](MERGE_DATA.md) functions for data import) and the function returns `[NumberOfChannels x resampleFactor*2^n]` samples. The impulse responses are windowed with a HANN window. The argument _win_ can take values from 0-1. Where 0 means that no window is applied and 1 will apply a window to the full IR. At a value of 0.5 the first half of the impulse responses keeps unchanged and the last half is multiplied with a HANN type window. The size of the window is fitted automatically. As default choice _win_ is set to 1/8 which should deliver good results in most of the cases. The impulse responses can be resampled to the original sampling rate before being downsampled in [readVSAdata()](READ_VSA.md) or [mergeArrayData()](MERGE_DATA.md). Set `resampleFactor = downSample` to get back to the original sample rate of the measurement source material. (**WARNING**: Matlab [Signal Processing Toolbox](http://www.mathworks.de/products/signal/) required for windowing and resampling)
<br><br>
To save processing power and calculation time the SOFiA chain works on the half-sided FFT spectrum only (NFFT/2+1). Therefore <a href='FDT.md'>F/D/T</a> produces  half-sided spectrum output signals (fftData). The <code>makeIR()</code> function automatically reconstructs the double-sided spectrum to compute the impulse responses.<br>
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/MAKEIR_NATIVE.png' />
<br>
<br>


<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> Y           </td><td> int         </td><td> Frequency domain data from <a href='PDC.md'>P/D/C</a> or <a href='ITC.md'>I/T/C</a> </td><td> --             </td></tr>
<tr><td> <i>win</i>  </td><td> float       </td><td> Window IR tail <code>[0-1]</code> with a HANN window </td><td> 1/8            </td></tr>
<tr><td> <i>resampleFactor</i> </td><td> int         </td><td> Resampling factor  </td><td> 1              </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> impulseResponses </td><td> float mtx   </td><td> Impulse Responses <br>Rows: IR-Data<br>Cols: Channels</td></tr></tbody></table>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_makeIR.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
impulseResponses = sofia_makeIR(Y, [win], [resampleFactor])<br>
------------------------------------------------------------------------     <br>
impulseResponses   Reconstructed impulse response<br>
                   Columns : Index / Channel: IR1, IR2, ... IRn<br>
                   Rows    : Impulse responses (time domain)<br>
------------------------------------------------------------------------              <br>
Y                  Frequency domain FFT data for multiple channels<br>
                   Columns : Index / Channel<br>
                   Rows    : FFT data (frequency domain)<br>
<br>
[win]              Window IR tail [0...1] with a HANN window<br>
                   0    off<br>
                   0-1  window coverage (1 full, 0 off)<br>
                   [default 1/8: 1/8 of the IR length is windowed]<br>
                   ! Signal Processing Toolbox required<br>
                  <br>
[resampleFactor]   Optional resampling: Resampling factor <br>
                   e.g. FS_target/FS_source<br>
                   Resampling is done using MATLAB RESAMPLE <br>
                   (See MATLAB documentation for more details)<br>
                   ! Signal Processing Toolbox required  <br>
<br>
 This function recombines impulse responses for multiple channels from<br>
frequency domain data. It is made to work with half-sided spectrum FFT <br>
data.  The impulse responses can be windowed.  The IFFT blocklength is <br>
determined by the Y data itself:<br>
<br>
Y should have a size [NumberOfChannels x ((2^n)/2)+1] with n=[1,2,3,...] <br>
and the function returns [NumberOfChannels x resampleFactor*2^n] samples.<br>
<br>
Dependencies: MATLAB Signal Processing Toolbox required for <br>
              windowing and resampling.    <br>
<br>
*/<br>
</code></pre>