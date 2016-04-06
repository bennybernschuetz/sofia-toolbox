# SOFiA application example 2 #

In the second example we generate a full audio spectrum unity plane wave of order N=5 impinging from Azimuth = 0 and Elevation = pi/2 to an open sphere array sampling on a 110 points Lebedev grid using [S/W/G](SWG.md). We observe the array responses in different fft-bins using [makeMTX](MAKE_MTX.md) and [visual3D](VISUAL_3D.md). Spatial aliasing artifacts arise at higher frequencies that destroy the plane wave response and produce very high output levels.

## File(s) ##

Run `sofiaAE2.m`.

## Output ##
![http://img.sofia-toolbox.googlecode.com/git/example2output.jpg](http://img.sofia-toolbox.googlecode.com/git/example2output.jpg)


## Code ##
```
/*
% SOFiA example 2: Sampled unity plane wave simulation for different kr  
% SOFiA Version  : R11-1220

  clear all
  clc
  
% Generate a full audio spectrum plane wave using S/W/G
   
  r    = 0.1;           % Array radius
  ac   = 0;             % Rigid Sphere
  FS   = 48000;         % Sampling Frequency
  NFFT = 128;           % FFT-Bin
  AZ   = 0*(pi/180);    % Azimuth angle
  EL   = 90*(pi/180);   % Elevation angle
  
  quadrature_grid = sofia_lebedev(110, 0);  %EXAMPLE GRID LEB110, No Plot

  [fftData, kr] = sofia_swg(r, quadrature_grid, ac, FS, NFFT, AZ, EL);

% Spatial Fourier Transform  

  Nsft = 5;      %Transform order  
  Pnm = sofia_stc(Nsft, fftData, quadrature_grid);

% Make radial filters 
  
  Nrf  = Nsft;   %Radial filter order
  dn   = sofia_mf(Nrf, kr, ac);

  
% Make visualization MTX  

  Nmtx = 5;
  krIndex = 15;   % Choose the kr-bin (Frequency) to display. 
  mtxDataLOW      = sofia_makeMTX(Nmtx, Pnm, dn, krIndex);
  
  krIndex = 24;   % Choose the kr-bin (Frequency) to display. 
  mtxDataMID      = sofia_makeMTX(Nmtx, Pnm, dn, krIndex);
  
  krIndex = 30;   % Choose the kr-bin (Frequency) to display. 
  mtxDataHIGH     = sofia_makeMTX(Nmtx, Pnm, dn, krIndex);
  
  krIndex = 40;   % Choose the kr-bin (Frequency) to display. 
  mtxDataVERYHIGH = sofia_makeMTX(Nmtx, Pnm, dn, krIndex);
  
  
 %Plot Responses for different kr (Example values)
 
  figure(1)
  clf();
  
  subplot(2,2,1)
  sofia_visual3D(mtxDataLOW, 0);      % Low Alias
  
  subplot(2,2,2)
  sofia_visual3D(mtxDataMID, 0);      % Some Alias
  
  subplot(2,2,3) 
  sofia_visual3D(mtxDataHIGH, 0);     % Strong Alias
  
  subplot(2,2,4)
  sofia_visual3D(mtxDataVERYHIGH, 0); % Extreme Alias
    
        
*/
```