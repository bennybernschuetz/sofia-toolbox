# SOFiA Sampled Wave Generator Wrapper #

The sampled wave generator emulates a full spectrum wave impact to a microphone array. The wave is sampled at discrete positions determined by a quadrature grid (e.g. from SOFiA\_lebedev() or SOFiA\_gauss()). The generator script can be modified to simulate errors like e.g. positioning or temperature deviation. Feeding the SOFiA chain with a S/W/G synthesized plane wave aliasing artifacts and errors can easily be simulated, visualized or auralized (see figures below). The S/W/G module (2nd generation) is a wrapper using the W/G/C wave generator core and the I/T/C inverse spatial fourier transform core. The internal generator order Ng should be (much) higher than the array order.
<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/SWG_WRAPPER.png' />
<br>
<br>

<h2>ARGUMENTS</h2>

<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> r           </td><td> float       </td><td> Microphone radius in m<br>Can also be a vector for rigid/dual sphere configurations:<br>(1,1) => rm  Microphone Radius <br>(2,1) => rs  Sphere Radius or Microphone2 Radius <br> ! If only one radius (rm) is given using a Rigid/Dual Sphere Configuration: <br> rs = rm. In this case only one kr-vector is returned. </td><td> 1              </td></tr>
<tr><td> q_grid      </td><td> float mtx   </td><td> Quadrature grid, positions and weights (W):<br>AZ<sub>1</sub> EL<sub>1</sub> W<sub>1</sub><br>AZ<sub>2</sub> EL<sub>2</sub> W<sub>2</sub><br> ...<br> AZ<sub>M</sub> EL<sub>M</sub> W<sub>M</sub> for M Positions </td><td> default: Lebedev 110P</td></tr>
<tr><td> ac          </td><td> int         </td><td> Array configuration <br> 0: Open Sphere with p Transducers <br>1: Open Sphere with pGrad Transducers <br>2: Rigid Sphere with p Transducers<br>3: Rigid Sphere with pGrad Transducers<br>4: Dual Open Sphere with p Transducers</td><td> 0              </td></tr>
<tr><td> FS          </td><td> int         </td><td> Sampling rate  </td><td> 48000          </td></tr>
<tr><td> NFFT        </td><td> int         </td><td> FFT Order (Number of bins) should be <code>2^x</code>, x=1,2,3,... </td><td> 512            </td></tr>
<tr><td> AZ          </td><td> float       </td><td> Azimuthal angle of the wave (Refer to <a href='COORDINATES.md'>Coordinate System</a>) </td><td> 0              </td></tr>
<tr><td> EL          </td><td> float       </td><td> Elevation angle of the wave (Refer to <a href='COORDINATES.md'>Coordinate System</a>) </td><td> pi/2           </td></tr>
<tr><td> <i>Ng</i>   </td><td> int         </td><td> Internal generator order  </td><td> 70             </td></tr>
<tr><td> <i>t</i>    </td><td> float       </td><td> Time delay in s</td><td> 0              </td></tr>
<tr><td> <i>c</i>    </td><td> float       </td><td> Speed of sound in m/s </td><td> 343.0          </td></tr>
<tr><td> <i>wavetype</i> </td><td> int         </td><td> 0: Plane wave, 1: Spherical wave  </td><td> 0              </td></tr>
<tr><td> <i>ds</i>   </td><td> float       </td><td> Source distance in m <br> (For wavetype = 1, spherical wave only) </td><td> 1m             </td></tr></tbody></table>


Angles AZ, EL are in RAD.<br>
<br>
<br>
<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> fftData     </td><td> complex float mtx </td><td> Frequency domain data for <a href='STC.md'>S/T/C</a></td></tr>
<tr><td> kr          </td><td> float vec   </td><td> kr Values (k: wave number, r: radius)<br> Can also be a matrix [krm; krs] for rigid sphere configurations: <br>[1,:] krm referring to the Microphone Radius <br>[2,:] krs referring to the Sphere/Microphone2 Radius   </td></tr></tbody></table>


<br>

<h2>ANALYSIS OF SPATIAL ALIASING USING SOFiA S/W/G</h2>
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/swg_responses.jpg' />

The figure shows array responses to a synhtesized plane wave from S/W/G for different kr-values. The left globe shows the response for <code>kr &lt;&lt; N</code>. Everything is fine. The globe in the middle is a response for <code>kr = N</code> (kr is slightly higher than N). Some spatial alias artifacts can be observed. The right one shows a response for <code>kr &gt;&gt; N</code>. The spatial aliasing has destroyed the plane wave response completely.<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/aliased_spectrum.jpg' />

The figure above shows a reconstructed spectrum for a full-spectrum (FS 48KHz) plane wave synthesized with the S/W/G module. The spectrum is perfectly reconstructed for all <code>kr&lt;N</code> but strong alias artifacts arise for <code>kr&gt;N</code> starting at 2-3KHz.<br>
<br>
<br>

<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_swg.m </td><td> Help header, Fuction </td><td> All OS    </td></tr></tbody></table>


<h2>HEADER</h2>
<pre><code>/*[fftdata, kr] = sofia_swg(r, q_grid, ac, FS, NFFT, ...<br>
                                      AZ, EL, Ng, t, c, wavetype, ds)<br>
------------------------------------------------------------------------<br>
fftData  Complex sound pressures                   [(N+1)^2 x NFFT]                              <br>
kr       kr-Vector <br>
         Can also be a matrix [krm; krs] for rigid sphere configurations:<br>
          [1,:] =&gt; krm referring to the Microphone Radius<br>
          [2,:] =&gt; krs referring to the Sphere/Microphone2 Radius  <br>
------------------------------------------------------------------------   <br>
r        Microphone Radius <br>
         Can also be a vector for rigid sphere configurations:<br>
          [1,1] =&gt; rm  Microphone Radius<br>
          [2,1] =&gt; rs  Sphere Radius (Scatterer)<br>
q_grid   Quadrature grid                           [default LEB110]<br>
          Columns : Position Number 1...M             <br>
          Rows    : [AZ EL Weight]<br>
          Angles AZ, EL in [RAD]<br>
ac       Array Configuration <br>
          0  Open Sphere with p Transducers <br>
          1  Open Sphere with pGrad Transducers<br>
          2  Rigid Sphere with p Transducers<br>
          3  Rigid Sphere with pGrad Transducers (Thx to Nils Peters!)<br>
          4  Dual Open Sphere with p Transducers (Thx to Nils Peters!)<br>
FS       Sampling Frequency<br>
NFFT     FFT Order (Number of bins) should be 2^x, x=1,2,3,... <br>
AZ       Azimuth   angle in [DEG] 0-2pi            <br>
EL       Elevation angle in [DEG] 0-pi <br>
Ng       Internal generator transform order. (Warning: Should be much<br>
         higher than typical microphone array orders) <br>
c        Speed of sound in [m/s] (Default: 343m/s)<br>
t        Time Delay in s <br>
wavetype Type of the Wave. 0: Plane Wave (default) 1: Spherical Wave <br>
ds       Distance of the source in [m] (For wavetype = 1 only)<br>
<br>
This file is a wrapper generating the complex pressures at the <br>
positions given in 'q_grid' for a full spectrum 0-FS/2 Hz (NFFT Bins) <br>
wave impinging to an array. The wrapper involves the W/G/C wave<br>
generator core and the I/T/C spatial transform core.<br>
*/<br>
</code></pre>