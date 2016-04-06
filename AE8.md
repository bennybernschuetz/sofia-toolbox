# SOFiA application example 8 #

In this example we render directional impulse responses from real array measurement data taken in a classroom, [Array Example 5](ARRAY_DATA.md). The original array data recorded at 44.1KHz is downsampled to 22.05KHz to avoid spatial aliasing. Later the IRs are resampled to 44.1KHz again (but of course there is no information >11KHz anymore!). The transform and decomposition orders are N=4 and we allow a maximum modal amplification of 10dB in this example.

![http://img.sofia-toolbox.googlecode.com/git/ROOM8W3_1.jpg](http://img.sofia-toolbox.googlecode.com/git/ROOM8W3_1.jpg)

## File(s) ##

Run `sofiaAE8.m`.
<br>
Locate the folder <code>EXAMPLE5_RealRoom</code> containing the required array data.<br>
<br>
<h2>Output</h2>
<img src='http://img.sofia-toolbox.googlecode.com/git/example8output.jpg' />


<h2>Code</h2>
<pre><code>/*<br>
% SOFiA example 8: Superdirective impulse responses   <br>
% SOFiA Version  : R11-1220<br>
% Array Dataset  : R11-1018<br>
<br>
  clear all<br>
  clc<br>
  <br>
% Read VariSphear dataset<br>
% !!! LOCATE THE FOLDER: "EXAMPLE5_RealRoom" <br>
<br>
  downsample = 2;<br>
  timeData = sofia_readVSAdata(downsample);<br>
<br>
% Transform time domain data to frequency domain and generate kr-vector<br>
  <br>
  [fftData, kr, f] = sofia_fdt(timeData);<br>
<br>
% Spatial Fourier Transform<br>
  Nsft = 4;<br>
  Pnm  = sofia_stc(Nsft, fftData, timeData.quadratureGrid);<br>
<br>
% Radial Filters for a rigid sphere array<br>
  Nrf      = Nsft;   % radial filter order               <br>
  maxAmp   = 10;     % Maximum modal amplification in [dB]<br>
  ac       = 2;      % Array configuration: 2 = Rigid Sphere <br>
  <br>
  dn                         = sofia_mf(Nrf , kr, ac, maxAmp);<br>
  [dn, kernelSize, latency]  = sofia_rfi(dn); % Radial Filter Improvement<br>
<br>
% Plane wave decomposition for directions given by OmegaL:<br>
  Npdc     = Nsft;   %Plane wave decomposition order<br>
  OmegaL   = [0 pi/2; pi pi/2];<br>
  Y        = sofia_pdc(Npdc, OmegaL, Pnm, dn);<br>
<br>
% Reconstruct directional impulse responses<br>
  impulseResponses = sofia_makeIR(Y, 1/8, downsample);<br>
  <br>
% Remove filter latency (Be careful, this is done very roughly here for <br>
% demonstrtion/visualisation purpose only)<br>
<br>
impulseResponses = impulseResponses(:, (latency*downsample):end);<br>
  <br>
  figure(1)<br>
  <br>
  tscale = linspace(0,size(impulseResponses,2)/(timeData.FS*downsample), size(impulseResponses,2));<br>
  <br>
  plot(tscale, impulseResponses')<br>
  title('Directional Impulse Responses')<br>
  xlabel('Time in s')<br>
  ylabel('Signal Amplitude')<br>
<br>
*/<br>
</code></pre>