# SOFiA application example 4 #

This example shows 4 plane waves of different SPL levels impinging to a real array in a rigid sphere configuration. We work on a real array dataset: [EXAMPLE 2](ARRAY_DATA.md). The four sources are different in level (45°:0dB, 15°:-3dB, 345°:-6dB, 315°:-9dB) and the "plane waves" arrive at the same time.

![http://img.sofia-toolbox.googlecode.com/git/ExperimentResolution.jpg](http://img.sofia-toolbox.googlecode.com/git/ExperimentResolution.jpg)

## File(s) ##

Run `sofiaAE4.m`.

Locate the folder `EXAMPLE2_LevelResolution` containing the required array data.

## Output ##
![http://img.sofia-toolbox.googlecode.com/git/example4output.jpg](http://img.sofia-toolbox.googlecode.com/git/example4output.jpg)
<br>
<b>Take care:</b> This figure shows a frontal view of the array response and the photo on top shows the rear side of the array.<br>
<br>
<br>
<h2>Code</h2>
<pre><code>/*<br>
% SOFiA example 4: Level/Space Resolution<br>
% SOFiA Version  : R11-1220<br>
% Array Dataset  : R11-1018<br>
<br>
  clear all<br>
  clc<br>
  <br>
% Read VariSphear dataset<br>
% !!! LOCATE THE FOLDER: "EXAMPLE2_LevelResolution" <br>
<br>
  timeData = sofia_readVSAdata(); <br>
<br>
% Transform time domain data to frequency domain and generate kr-vector   <br>
<br>
[fftData, kr, f] = sofia_fdt(timeData);<br>
    <br>
% Spatial Fourier Transform<br>
<br>
Nsft = 5;<br>
Pnm  = sofia_stc(Nsft, fftData, timeData.quadratureGrid);<br>
<br>
% Radial Filters for a rigid sphere array <br>
<br>
Nrf      = Nsft;    % radial filter order              <br>
maxAmp   = 10;      % Maximum modal amplification in [dB]<br>
ac       = 2;       % Array configuration: 2 = Rigid Sphere <br>
<br>
dn       = sofia_mf(Nrf , kr, ac, maxAmp); % radial filters <br>
dn       = sofia_rfi(dn);                  % radial filter improvement<br>
<br>
% Make MTX  <br>
<br>
Nmtx = Nsft;<br>
krIndex = 600;   % Here we select the kr-bin (Frequency) to display. <br>
mtxData = sofia_makeMTX(Nmtx, Pnm, dn, krIndex);<br>
      <br>
<br>
% Plot the response<br>
<br>
figure(1)<br>
clf();<br>
<br>
sofia_visual3D(mtxData, 0);<br>
view(90,0)    <br>
        <br>
disp(' ');<br>
disp(['The plot shows the response at a frequency of ',num2str(round(10*f(krIndex))/10),'Hz']);<br>
*/<br>
</code></pre>