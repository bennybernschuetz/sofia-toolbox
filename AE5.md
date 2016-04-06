# SOFiA application example 5 #

This example shows 4 "plane waves" impinging to a real array in a rigid sphere configuration that arrive at different times. We work on a real array dataset: [EXAMPLE 3](ARRAY_DATA.md). The four sources have the same level but different time delays (45°:0ms, 15°:16ms, 345°:32ms, 315°:48ms). This example shows how to get access to the spatiotemporal sound field information running a plane wave decomposition on different time windows.

![http://img.sofia-toolbox.googlecode.com/git/ExperimentResolution.jpg](http://img.sofia-toolbox.googlecode.com/git/ExperimentResolution.jpg)

## File(s) ##

Run `sofiaAE5.m`.

Locate the folder `EXAMPLE3_SpatioTemporal` containing the required array data.

## Output ##
![http://img.sofia-toolbox.googlecode.com/git/example5output.jpg](http://img.sofia-toolbox.googlecode.com/git/example5output.jpg)
<br>
<b>Take care:</b> This figure shows frontal views of the array response and the photo on top shows the rear side of the array.<br>
<br>
<br>
<h2>Code</h2>
<pre><code>/*<br>
% SOFiA example 5: Spatiotemporal resolution<br>
% SOFiA Version  : R11-1220<br>
% Array Dataset  : R11-1018<br>
<br>
  clear all<br>
  clc<br>
  <br>
% Read VariSphear dataset<br>
% !!! LOCATE THE FOLDER: "EXAMPLE3_SpatioTemporal" <br>
<br>
  timeData = sofia_readVSAdata(); <br>
 <br>
% figure(2) %Enable to get an IR overview<br>
% clf();<br>
% area(timeData.irOverlay');<br>
<br>
  fftOversize = 2;<br>
  startSample = [400 1100 1800 2500]; %Examplary values (Enable area plot)<br>
  blockSize   = 256;<br>
<br>
  figure(1)<br>
  clf();<br>
  <br>
for ctr=1:size(startSample,2) <br>
      <br>
% Here we have simply put a loop around, because this is good for<br>
% understanding this experiment. The loop content can easily be optimized. <br>
   <br>
  % Transform time domain data to frequency domain and generate kr-vector<br>
  <br>
  [fftData, kr, f] = sofia_fdt(timeData, fftOversize, startSample(ctr), startSample(ctr)+blockSize);<br>
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
    dn       = sofia_mf(Nrf , kr, ac, maxAmp); % radial filters <br>
<br>
    % Make MTX  <br>
    <br>
    Nmtx = Nsft;<br>
    krIndex = 90;   % Choose the kr-bin (Frequency) to display. <br>
    mtxData = sofia_makeMTX(Nmtx, Pnm, dn, krIndex);<br>
  <br>
    subplot(2,2,ctr)<br>
    sofia_visual3D(mtxData, 0);<br>
    view(90,0)    <br>
        <br>
end<br>
  <br>
  disp(['The plot shows responses at a frequency of ',num2str(round(10*f(krIndex))/10),'Hz']);<br>
<br>
*/<br>
</code></pre>