# SOFiA Modal Radial Filters #

SOFiA M/F is a modal radial filter core for spherical microphone arrays. M/F can generate filters for different sphere and microphone configurations and involves soft-limiting of the mode amplification and free field powerloss compensation.
<br>
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/MF_CORE.png' />
<br>
<br>

<h2>ARGUMENTS</h2>
<b>Input</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th><th> <b>Default</b> </th></thead><tbody>
<tr><td> N           </td><td> int         </td><td> Maximum filter order to be generated </td><td> --             </td></tr>
<tr><td> kr          </td><td> float vec <br> or float mtx </td><td> Vector or Matrix of kr values <br>First Row (M=1) N: kr values Microphone Radius <br> Second Row  (M=2) N: kr values Sphere/Microphone2 Radius <br>[kr_mic;kr_sphere] or [kr_1; kr_2] for Rigid/Dual Sphere Configurations. <br> If only one kr-vector is given using a Rigid/Dual Sphere Configuration: kr_sphere = kr_mic  </td><td> --             </td></tr>
<tr><td> ac          </td><td> int         </td><td> Array configuration <br> 0: Open Sphere with p Transducers (No PLC!)<br>1: Open Sphere with pGrad Transducers <br>2: Rigid Sphere with p Transducers<br>3: Rigid Sphere with pGrad Transducers (Thanx to Nils Peters!)<br>4: Dual Open Sphere with p Transducers (Thanx to Nils Peters!)</td><td> ---            </td></tr>
<tr><td> <i>a_max</i></td><td> float       </td><td> Maximum mode amplification in dB </td><td> ---            </td></tr>
<tr><td> <i>plc</i>  </td><td> int         </td><td> Free field powerloss compensation <br> 0: Off <br> 1: Full kr-spectrum plc <br> 2: Low kr only -> set fadeover </td><td> ---            </td></tr>
<tr><td> <i>fadeover</i> </td><td> int         </td><td> Number of kr values to fade over +/- around min-distance gap of powerloss <br> compensated filter and normal N0 filters. 0 = auto fadeover </td><td> ---            </td></tr></tbody></table>

<b>Output</b>
<table><thead><th> <b>Name</b> </th><th> <b>Type</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> dn          </td><td> complex float mtx </td><td> Frequency domain radial filter coefficients </td></tr>
<tr><td> beam        </td><td> complex float vec </td><td> Free field kr-Response <br>Plot it with <code>semilogx(20*log10(abs(beam')))</code> </td></tr></tbody></table>


<h2>DEFINITIONS</h2>
The d<sub>n</sub> coefficients are defined as:<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/DN1_FORMULA.png' /><br>
Where b<sub>n</sub> depends on the sphere configuration and microphone type:<br><br>
<b>AC0 Open sphere with pressure transducers:</b><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/OPEN_FORMULA.png' /><br>
<b>AC1 Open sphere with pressure gradient transducers (cardioids):</b><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/CARDIOID_FORMULA.png' /><br>
<b>AC2 Rigid sphere with pressure transducers:</b><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/RIGID_FORMULA.png' /><br>
<br>
Configurations AC3 and AC4 are contributed and implemented by Nils Peters:<br><br>
<b>AC3 Rigid sphere with pressure gradient transducers (cardioids):</b><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/CARDISPHERE_FORMULA.png' /><br>
<b>AC4 Dual open sphere with pressure transducers:</b><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/DUALSPHERE_FORMULA.png' /><br>

<i>j<sub>n</sub>(kr)</i> denotes the spherical bessel function of the first kind,  <i>h<sub>n</sub>(kr)</i> <br> the spherical hankel function of the second kind and i=sqrt(-1).<br>
<br>
<b>When modal amplification limiting is enabled, d<sub>n</sub> is defined as:</b> <br>
<img src='http://img.sofia-toolbox.googlecode.com/git/DN2_FORMULA.png' /><br>

<b>Powerloss free-field filters:</b><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/PLC1_FORMULA.png' /><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/PLC2_FORMULA.png' /><br>



<h2>BASIC RADIAL FILTERS</h2>

<img src='http://img.sofia-toolbox.googlecode.com/git/RADIAL_FILTERS.png' /><br>
The plots show basic radial filters (no limiting, no plc) for N=5 and different array configurations (ac): ac=0 Open Sphere with pressure transducers, ac=1 Open Sphere with pressure gradient transducers (cardioid), ac=2 Rigid Sphere with pressure transducers, ac=3 Open Sphere with gradient transducers (cardioid) and ac=4 Dual Open Sphere with pressure transducers.<br>
<br>
<h2>SOFT-LIMITING OF THE MODE AMPLIFICATION</h2>
At low kr the modes have to be amplified very hard (see figure above). In real array datasets this required amplification cannot be achieved as the singnal to noise ratio is limited. Strong amplification would raise more noise then useful signal contribution and disturb the array output signal. Therefore the mode amplification has to be limited to reasonable values in real life. This should not be done with hard limits as hard limiting leads to artifacts in the spatial domain. SOFiA M/F therfore uses soft-knee limitation.<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/LIMITING1.png' /><br>

<img src='http://img.sofia-toolbox.googlecode.com/git/LIMITING2.png' /><br>

The left figures (a) show hard limiting and the right ones (b) soft limiting. Both filtersets are limited to to +40dB <br>

The following figure shows a real measured array response to a plane wave with basic radial filters in the upper row and SOFiA soft-limited radial filters in the bottom row. The response for low kr using basic radial filters is disrupted due to measurement noise. The soft-limited response looses directivity (as expected) but keeps stable.<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/LIMITER_REAL1.png' /><br>


<h2>BEAM RESPONSE</h2>

The modal amplification limiting has influence on the kr-response (which can be seen as the array's frequency response). The kr-response can be controlled by plotting the return vector <code>beam</code> e.g. with <code>semilogx(20*log10(abs(beam')))</code>. <br>

<img src='http://img.sofia-toolbox.googlecode.com/git/BEAM_CONTROL.png' /><br>


<h2>FREE FIELD PLC</h2>
In a free field the kr-response can be aligned using the N0 mode which offers a good signal to noise ratio. This is called plc (powerloss compensation). The plc leads to a perfect on-axis kr-response. The plc compensation can be applied to the full spectrum or be limited to low frequencies only. In the last case M/F will fade the compensated filter to normal N0 filters at their minimum distance.<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/PLC1.png' /><br>
<img src='http://img.sofia-toolbox.googlecode.com/git/PLC2.png' /><br>

The figure shows the array's azimutal response to a full kr-spectrum plane wave coming from 180°. The response is compensated on axis but other directions have a raised sensitivity to low frequencies. This leads to an over-emphasized low frequency response in diffuse fields.<br>
<br><br>


<h2>FILE(S):</h2>

<table><thead><th> File </th><th> Type </th><th> OS/Matlab </th></thead><tbody>
<tr><td> sofia_mf.m </td><td> Help header </td><td> All OS    </td></tr>
<tr><td> sofia_mf.mexmaci64 </td><td> MEX core </td><td> OS-X Intel </td></tr>
<tr><td> sofia_mf.mexw32 </td><td> MEX core </td><td> Windows, MATLAB32 </td></tr>
<tr><td> sofia_mf.mexw64 </td><td> MEX core </td><td> Windows, MATLAB64 </td></tr>
<tr><td> sofia_mf.cpp </td><td> C/C++ source </td><td> All OS    </td></tr>
<tr><td> sofia_radial.h </td><td> internal C/C++ header </td><td> All OS    </td></tr>
<tr><td> sofia_radial.cpp </td><td> internal C/C++ header/source </td><td> All OS    </td></tr></tbody></table>

<h2>HEADER</h2>
<pre><code>/*<br>
[dn, beam] = SOFIA_MF(N, kr, ac, [a_max], [plc], [fadeover])<br>
------------------------------------------------------------------------   <br>
dn          Vector of modal 0-N frequency domain filters<br>
beam        Expected free field On-Axis kr-response <br>
------------------------------------------------------------------------<br>
N           Maximum Order<br>
kr          Vector or Matrix of kr values<br>
            First Row   (M=1) N: kr values Microphone Radius<br>
            Second Row  (M=2) N: kr values Sphere/Microphone2 Radius <br>
            [kr_mic;kr_sphere] for Rigid/Dual Sphere Configurations<br>
            ! If only one kr-vector is given using a Rigid/Dual Sphere  <br>
            Configuration: kr_sphere = kr_mic <br>
ac          Array Configuration: <br>
            0  Open Sphere with p Transducers (NO plc!)<br>
            1  Open Sphere with pGrad Transducers<br>
            2  Rigid Sphere with p Transducers<br>
            3  Rigid Sphere with pGrad Transducers (Thx to Nils Peters!)<br>
            4  Dual Open Sphere with p Transducers (Thx to Nils Peters!)<br>
a_max       Maximum modal amplification limit in [dB]<br>
plc         OnAxis powerloss-compensation: <br>
            0  Off<br>
            1  Full kr-spectrum plc<br>
            2  Low kr only -&gt; set fadeover             <br>
fadeover    Number of kr values to fade over +/- around min-distance <br>
            gap of powerloss compensated filter and normal N0 filters.<br>
            0 = auto fadeover<br>
*/<br>
</code></pre>

The M/F core involves Bessel and Hankel functions provided by the peer-reviewed <a href='http://www.boost.org'>BOOST C++ Math Library</a> under the <a href='http://www.boost.org/LICENSE_1_0.txt'>BOOST Software License</a>.