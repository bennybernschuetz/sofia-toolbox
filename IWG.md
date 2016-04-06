# SOFiA ideal wave generator #

The I/W/G ideal wave generator emulates a plane wave with unity magnitude impinging to a microphone array. The script delivers ideal Fourier coefficients. I/W/G can emulate different array/microphone configurations.
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/IWG_NATIVE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> N           </td><td> int         </td><td> Maximum order   </td><td>  10            </td></tr>
<tr><td> r           </td><td> float       </td><td> Array radius in m </td><td> 1.0            </td></tr>
<tr><td> ac          </td><td> int         </td><td> Array configuration (0,1,2) <br> 0: Open Sphere with p Transducers (NO plc!)<br>1: Open Sphere with pGrad Transducers <br>2: Rigid Sphere with p Transducers</td><td> 0              </td></tr>
<tr><td> FS          </td><td> int         </td><td> Sampling rate in Hz </td><td> 48000          </td></tr>
<tr><td> NFFT        </td><td> int         </td><td> FFT Order (Number of bins) should be <code>2^x</code>, x=1,2,3,... </td><td> 512            </td></tr>
<tr><td> AZ          </td><td> float       </td><td> Azimutal angle in radians<br>Refer to <a href='COORDINATES.md'>Coordinate System</a>  </td><td> 0              </td></tr>
<tr><td> EL          </td><td> float       </td><td> Elevation angle in radians<br>Refer to <a href='COORDINATES.md'>Coordinate System</a> </td><td> pi/2           </td></tr></tbody></table>

Angles AZ, EL are in RAD.<br>
<br>
<br>
<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> fftData     </td><td> complex float mtx <code>[(N+1)^2 x NFFT/2+1]</code>  </td><td> Frequency domain data for <a href='STC.md'>S/T/C</a></td></tr>
<tr><td> kr          </td><td> float vec <code>[1 x NFFT/2+1]</code></td><td> kr Values (k: wave number, r: radius) </td></tr></tbody></table>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_iwg.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*<br>
[Pnm, kr] = sofia_iwg(N, r, ac, FS, NFFT, AZ, EL) <br>
------------------------------------------------------------------------     <br>
Pnm     Spatial Fourier Coefficients              [(N+1)^2 x NFFT]<br>
kr      kr values                                 [      1 x NFFT]<br>
------------------------------------------------------------------------              <br>
N       Maximum order                             [default = 10]<br>
r 	Simulation radius in [m] (array radius)   [default = 1]  <br>
ac      Array Configuration [0,1,2]               [default = 0] <br>
        0 - Open Sphere with p Transducers<br>
        1 - Open Sphere with pGrad Transducers<br>
        2 - Rigid Sphere with p Transducers<br>
FS      Sampling rate [1/s]                       [default = 48000]<br>
NFFT    Number of FFT bins                        [default = 512]<br>
AZ      Azimuth   angle in [DEG] 0-2pi            [default = 0]<br>
WL      Elevation angle in [DEG] 0-pi             [default = pi/2]<br>
*/<br>
</code></pre>