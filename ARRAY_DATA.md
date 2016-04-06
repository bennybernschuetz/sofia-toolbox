# Array datasets R 11-1018 #
In the [download section](http://code.google.com/p/sofia-toolbox/downloads/list) we provide some example datasets to get familiar with SOFiA and to evaluate it. There are different scenarios taken in an anechoic chamber and in "real" rooms as listed below. Some of the [application examples](EXAMPLES.md) are based on that measurement data. All datasets are captured with a VariSphear spherical array measurement system, RME microphone  preamplifiers and RME Hammerfall HDSP II audio interfaces. Different microphones and sources were used and are specified below.

The datasets can be imported to SOFiA using the [readVSAdata()](READ_VSA.md) module.

<a href='http://creativecommons.org/licenses/by-sa/3.0/'><img src='http://i.creativecommons.org/l/by-sa/3.0/88x31.png' alt='Creative Commons Lizenzvertrag' /></a><br>

The SOFiA Array Datasets (Copyright 2011 by Benjamin Bernschütz as a representative of the ASAR-Research Group) are licensed under a <a href='http://creativecommons.org/licenses/by-sa/3.0/'>Creative Commons Attribution 3.0 License</a>.<br>
<br>
<br>
<h2>Overview</h2>

<table><thead><th> <b>Number</b> </th><th> <b>Location</b> </th><th> <b>Sources</b> </th><th> <b>Mic/Sphere Configuration</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> 1             </td><td> Anechoic Chamber </td><td> 4              </td><td> Omni, Rigid Sphere              </td><td> Spatial Resolution </td></tr>
<tr><td> 2             </td><td> Anechoic Chamber </td><td> 4              </td><td> Omni, Rigid Sphere              </td><td> Level Resolution </td></tr>
<tr><td> 3             </td><td> Anechoic Chamber </td><td> 4              </td><td> Omni, Rigid Sphere              </td><td> Spatiotemporal Resolution </td></tr>
<tr><td> 4             </td><td> Anechoic Chamber </td><td> 1              </td><td> Cardioid, Open Sphere           </td><td> Cardioid Example </td></tr>
<tr><td> 5             </td><td> Real Room       </td><td> 1 (Omni)       </td><td> Omni/Rigid Sphere               </td><td> Real scenario  </td></tr></tbody></table>


<h2>Example 1-3</h2>
For the examples 1-3 we have placed 4 sources (Genelec 1029A active 2-Way Speakers) in a circle of 2.5 meters radius and an angle spread of 30° around the array in an anechoic chamber (Room 8W4 at the Cologne University of Applied Sciences). The elevation is fixed at pi/2 (90°). The speakers were calibrated to deliver approximately identical sound pressure levels at the array position. They were driven thru a XTA DP224 PA speaker management system to apply different level and delay shifts.<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/ExperimentResolution.jpg' />
<br>

<img src='http://img.sofia-toolbox.googlecode.com/git/XTA_waveCapture.jpg' />

<b>Technical specs</b>

<table><thead><th> <b>Number</b> </th><th> <b>Location</b> </th><th> <b>Microphone</b> </th><th> <b>Sphere Configuarion</b> </th><th> <b>Source(s)</b> </th><th> <b>Grid</b> </th></thead><tbody>
<tr><td> 1             </td><td> Anechoic Chamber </td><td> Earthworks M30 Omni </td><td> Rigid Sphere d=17.5cm      </td><td> 4xGenelec1029A   </td><td> Lebedev 110P </td></tr>
<tr><td> 2             </td><td> Anechoic Chamber </td><td> Earthworks M30 Omni </td><td> Rigid Sphere d=17.5cm      </td><td> 4xGenelec1029A   </td><td> Lebedev 110P </td></tr>
<tr><td> 3             </td><td> Anechoic Chamber </td><td> Earthworks M30 Omni </td><td> Rigid Sphere d=17.5cm      </td><td> 4xGenelec1029A   </td><td> Lebedev 110P </td></tr></tbody></table>

<b>Level differences and timing</b> (From left to right as depicted in the figure above)<br>
<br>
<table><thead><th> <b>Number</b> </th><th> <b>Level Differences</b><br><b>(45° 15° 345° 315°)</b> </th><th> <b>Delays</b><br><b>(45° 15° 345° 315°)</b> </th><th> <b>Purpose</b> </th></thead><tbody>
<tr><td> 1             </td><td> 0dB 0dB 0dB 0dB                                        </td><td> 0ms 0ms 0ms 0ms                             </td><td> Four  "plane waves" arriving at the same time with the same level.</td></tr>
<tr><td> 2             </td><td> 0dB -3dB -6dB -9dB                                     </td><td> 0ms 0ms 0ms 0ms                             </td><td> Four "plane waves" arriving at the same time but different in level.</td></tr>
<tr><td> 3             </td><td> 0dB 0dB 0dB 0dB                                        </td><td> 0ms 16ms 32ms 48ms                          </td><td> Four  "plane waves" arriving at different times with the same level.</td></tr></tbody></table>

<h2>Example 4</h2>
Example 4 is a dataset to evaluate a cardioid setup involving a Microtech Gefell M900 large diaphragm microphone. The source was a AD-Systems Flex15 PA Speaker with AD-Systems Impulse D1 system amplifier and was placed at a distance of approximately 4m to the array. The dataset was captured in the anechoic chamber.<br>
<br>
<b>Technical specs</b>

<table><thead><th> <b>Number</b> </th><th> <b>Location</b> </th><th> <b>Microphone</b> </th><th> <b>Sphere Configuarion</b> </th><th> <b>Source(s)</b> </th><th> <b>Grid</b> </th></thead><tbody>
<tr><td> 4             </td><td> Anechoic Chamber </td><td> Microtech Gefell M900 cardioid </td><td> Open sphere r=25.0cm       </td><td> 1xAD-Systems Flex15 </td><td> Lebedev 86P </td></tr></tbody></table>

<h2>Example 5</h2>
Example 5 delivers measurement data from a real room. This is a common classroom with a volume of approx. 500m<sup>3</sup> and a surface of approx. 500m<sup>2</sup> (Measures: 20m x 8.5m x 3m). The mean RT60 is around 0.9s. Source and array were placed at a distance of 8m from each other. The source is a high power DSP-controlled 3-way dodecahedron (<i>Sonic Ball</i>) developed at the Cologne University of Applied Sciences wich offers a good omnidirectional radiation at the full audio bandwith.<br>
<br>
<br>
<img src='http://img.sofia-toolbox.googlecode.com/git/ROOM8W3_1.jpg' />

<b>Technical specs</b>

<table><thead><th> <b>Number</b> </th><th> <b>Location</b> </th><th> <b>Microphone</b> </th><th> <b>Sphere Configuarion</b> </th><th> <b>Source(s)</b> </th><th> <b>Grid</b> </th></thead><tbody>
<tr><td> 5             </td><td> Real Room (Classroom) </td><td> Earthworks M30 Omni </td><td> Rigid Sphere d=17.5cm      </td><td> Sonic Ball (Omnidirectional) </td><td> Lebedev 590P </td></tr>