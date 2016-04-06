# SOFiA Wave Generator Core #

The W/G/C Wave Generator Core delivers ideal analytical fourier coefficients emulating a full spectrum (0-FS/2) wave impact to an array.
<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/WGC_CORE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> N           </td><td> int         </td><td> Maximum order   </td><td>  ---           </td></tr>
<tr><td> r           </td><td> float       </td><td> Microphone radius in m<br>Can also be a vector for rigid/dual sphere configurations:<br>(1,1) => rm  Microphone Radius <br>(2,1) => rs  Sphere Radius or Microphone2 Radius <br> ! If only one radius (rm) is given using a Rigid/Dual Sphere Configuration: <br> rs = rm. In this case only one kr-vector is returned. </td><td> ---            </td></tr>
<tr><td> ac          </td><td> int         </td><td> Array configuration <br> 0: Open Sphere with p Transducers <br>1: Open Sphere with pGrad Transducers <br>2: Rigid Sphere with p Transducers<br>3: Rigid Sphere with pGrad Transducers<br>4: Dual Open Sphere with p Transducers</td><td> ---            </td></tr>
<tr><td> FS          </td><td> int         </td><td> Sampling rate  </td><td> ---            </td></tr>
<tr><td> NFFT        </td><td> int         </td><td> FFT Order (Number of bins) should be <code>2^x</code>, x=1,2,3,... </td><td> ---            </td></tr>
<tr><td> AZ          </td><td> float       </td><td> Azimuthal angle of the wave (Refer to <a href='COORDINATES.md'>Coordinate System</a>) </td><td> ---            </td></tr>
<tr><td> EL          </td><td> float       </td><td> Elevation angle of the wave (Refer to <a href='COORDINATES.md'>Coordinate System</a>) </td><td> ---            </td></tr>
<tr><td> <i>t</i>    </td><td> float       </td><td> Time delay in s</td><td> 0              </td></tr>
<tr><td> <i>c</i>    </td><td> float       </td><td> Speed of sound in m/s </td><td> 343.0          </td></tr>
<tr><td> <i>wavetype</i> </td><td> int         </td><td> 0: Plane wave, 1: Spherical wave  </td><td> 0              </td></tr>
<tr><td> <i>ds</i>   </td><td> float       </td><td> Source distance in m (For wavetype = 1, spherical wave only) <br>Warning: If NFFT is smaller than the time the wavefront needs <br> to travel from the source to the array, the impulse response will by <br> cyclically shifted (cyclic convolution). </td><td> 1m             </td></tr></tbody></table>


Angles AZ, EL are in RAD.<br>
<br>
<br>
<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> fftData     </td><td> complex float mtx <code>[(N+1)^2 x NFFT/2+1]</code>  </td><td> Frequency domain data for <a href='STC.md'>S/T/C</a></td></tr>
<tr><td> kr          </td><td> float vec <code>[1 x NFFT/2+1]</code><br> or float mtx <code>[2 x NFFT/2+1]</code></td><td> kr-Vector (k: wave number, r: radius)<br>Can also be a matrix [krm; krs] for rigid sphere configurations:<br>(1,:) => krm referring to the Microphone Radius<br>(2,:) => krs referring to the Sphere Radius (Scatterer)</td></tr></tbody></table>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_wgc.m </td><td> Help header </td><td> All OS    </td></tr>
<tr><td> sofia_wgc.mexmaci64 </td><td> MEX core </td><td> OS-X Intel </td></tr>
<tr><td> sofia_wgc.mexw32 </td><td> MEX core </td><td> Windows, MATLAB32 </td></tr>
<tr><td> sofia_wgc.mexw64 </td><td> MEX core </td><td> Windows, MATLAB64 </td></tr>
<tr><td> sofia_wgc.cpp </td><td> C/C++ source </td><td> All OS    </td></tr>
<tr><td> sofia_radial.h </td><td> internal C/C++ header </td><td> All OS    </td></tr>
<tr><td> sofia_radial.cpp </td><td> internal C/C++ header/source </td><td> All OS    </td></tr></tbody></table>

<h2>HEADER</h2>
<pre><code>/*<br>
[Pnm, kr] = sofia_wgc(N, r, ac, FS, NFFT, AZ, EL, <br>
                            t, c, wavetype, ds, lSegLim, uSegLim, SeqN)<br>
------------------------------------------------------------------------<br>
Pnm      Spatial Fourier Coefficients <br>
         Columns : nm coeff<br>
         Rows    : FFT bins <br>
kr       kr-Vector <br>
         Can also be a matrix [krm; krs] for rigid sphere configurations:<br>
         [1,:] =&gt; krm referring to the Microphone Radius<br>
         [2,:] =&gt; krs referring to the Sphere Radius (Scatterer)<br>
 <br>
------------------------------------------------------------------------   <br>
N        Maximum transform order<br>
r        Microphone Radius <br>
         Can also be a vector for rigid/dual sphere configurations:<br>
         [1,1] =&gt; rm  Microphone Radius <br>
         [2,1] =&gt; rs  Sphere Radius or Microphone2 Radius<br>
         ! If only one radius (rm) is given using a Rigid/Dual Sphere  <br>
           Configuration: rs = rm and only one kr-vector is returned!<br>
ac       Array Configuration <br>
         0  Open Sphere with p Transducers (NO plc!)<br>
         1  Open Sphere with pGrad Transducers<br>
         2  Rigid Sphere with p Transducers<br>
         3  Rigid Sphere with pGrad Transducers (Thx to Nils Peters!)<br>
         4  Dual Open Sphere with p Transducers (Thx to Nils Peters!)<br>
FS       Sampling Frequency<br>
NFFT     FFT Order (Number of bins) should be 2^x, x=1,2,3,... <br>
AZ       Azimuth   angle in [DEG] 0-2pi            <br>
EL       Elevation angle in [DEG] 0-pi                   <br>
c        Speed of sound in [m/s] (Default: 343m/s)<br>
t        Time Delay in s. The delay has: (t*FS) Samples<br>
wavetype Type of the Wave. 0: Plane Wave (default) 1: Spherical Wave <br>
ds       Distance of the source in [m] (For wavetype = 1 only)<br>
         Warning: If NFFT is smaller than the time the wavefront <br>
         needs to travel from the source to the array, the impulse <br>
         response will by cyclically shifted (cyclic convolution). <br>
---<br>
lSegLim  (Lower Segment Limit) Used by the S/W/G wrapper<br>
uSegLim  (Upper Segment Limit) Used by the S/W/G wrapper<br>
SegN     (Sement Order)        Used by the S/W/G wrapper<br>
<br>
*/<br>
</code></pre>