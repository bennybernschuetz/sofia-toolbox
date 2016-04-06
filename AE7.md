# SOFiA application example 7 #

In this example we simulate a plane wave impact to a rigid sphere array sampling at discrete positions using S/W/G. We render impulse responses for two different pwd directions. Play around with the configurations to observe the influence of spatial aliasing.


## File(s) ##

Run `sofiaAE7.m`.

## Output ##
![http://img.sofia-toolbox.googlecode.com/git/example7output.jpg](http://img.sofia-toolbox.googlecode.com/git/example7output.jpg)
<br>

<h2>Code</h2>
<pre><code>/*<br>
% SOFiA example 7: Impulse response reconstruction on a simulated <br>
%                  sampled unity plane wave.<br>
% SOFiA Version  : R11-1220<br>
<br>
  clear all<br>
  clc<br>
  <br>
% Generate a full audio spectrum plane wave using S/W/G<br>
   <br>
  r    = 0.2;             % Array radius<br>
  ac   = 2;               % Rigid Sphere Array<br>
  FS   = 24000;           % Sampling Frequency<br>
  NFFT = 1024;            % FFT-Bins<br>
  AZ   = 0;               % Azimuth angle<br>
  EL   = pi/2;            % Elevation angle<br>
  <br>
  quadrature_grid = sofia_lebedev(110, 0);  %EXAMPLE GRID LEB110, No Plot<br>
 <br>
  [fftData, kr] = sofia_swg(r, quadrature_grid, ac, FS, NFFT, AZ, EL);<br>
<br>
% Spatial Fourier Transform  <br>
<br>
  Nsft = 5;                     % Transform order  <br>
  Pnm = sofia_stc(Nsft, fftData, quadrature_grid);<br>
<br>
% Make radial filters <br>
<br>
  Nrf  = Nsft;                  % radial filter order<br>
  limit = 150;                  % Amplification Limit (Keep the result<br>
                                % numerical stable at low frequencies)<br>
  <br>
  dn   = sofia_mf(Nrf, kr, ac, limit);<br>
  <br>
% Running a plane wave decomposition for different look directions<br>
  <br>
  Npdc   = Nsft;                 % Decomposition order<br>
  OmegaL = [0 pi/2; pi/2 pi/2];  % Looking towards the wave and to one side<br>
  <br>
  Y = sofia_pdc(Npdc, OmegaL, Pnm, dn);<br>
  <br>
% Reconstruct impulse responses<br>
<br>
  impulseResponses = sofia_makeIR(Y,0);<br>
    <br>
% Make IR causal:<br>
<br>
  impulseResponses = [impulseResponses(:,end/2+1:end), impulseResponses(:,1:end/2)];<br>
  <br>
% Plot results (Impulse Responses)<br>
<br>
  figure(1)  <br>
  subplot(1,2,1)<br>
  plot(impulseResponses')<br>
  title('Impulse response');<br>
  xlabel('Samples');<br>
  ylabel('Amplitude');<br>
  <br>
  axis([-100 NFFT -0.2 1.2])<br>
  grid on<br>
<br>
% Plot results (Spectra)<br>
<br>
  spectrum = abs(fft(impulseResponses'));<br>
  fscale = FS/2*linspace(0,1,NFFT/2+1);<br>
  <br>
  subplot(1,2,2)<br>
  semilogx(fscale,20*log10(spectrum(1:end/2+1,:)))<br>
  title('Spectrum');<br>
  xlabel('Frequency in Hz')<br>
  ylabel('Magnitude');  <br>
  axis([50 FS/2 -60 30])<br>
  grid on<br>
<br>
*/<br>
</code></pre>