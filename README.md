# Daylight Factor (DF) computation
The code file stored in this repository computes the mean & median Daylight Factor values over a grid of points (0.2m resolution) placed 0.8m above the floor area of a living room on different floors. 

<br>
<br>

## Daylight Factor definition:
The Daylight Factor is defined as the percentage ratio of the illuminance in a room compared to the illuminance on a horizontal plane under an unobstructed hemisphere with an overcast sky (Dubois et al., 2019).

<br>
<br>

<p align="center"><img src="img//daylight_factor.png" width=70%></img></p>

<br>
<br>

## Input data:
- 3D city model including detailed building exterior and interior information (equivalent to CityGML LOD4) like e.g. floor surface, windows, room ceiling, balconies, balcony railings, etc. 

<br>
<p align="center"><img src="img//building_model.PNG" width=70%></img></p>


<br>
<br>

## Requirements:

- An installed version of [Rhino 7](https://www.rhino3d.com/) with the following tools:
  - [Climate Studio](https://www.solemma.com/climatestudio?gclid=Cj0KCQiA6fafBhC1ARIsAIJjL8mMBqtiBLklABOnztZ7fa2CbLVZGWax759uG0MbsUMTqEaSxicNspUaAr9SEALw_wcB)


<br>
<br>

## Workflow:
The process depicted in this workflow computes the mean & median Daylight Factor values over a grid of points (0.2m resolution) placed 0.8m above the floor area of a living room on different floors. The aforementioned process also calculates the min and max DF-values of a room along with the % of the floor area that complies to the daylight requirement stated in the [Swedish legislation (DF > 1%)](https://www.boverket.se/globalassets/publikationer/dokument/2019/bbr-2011-6-tom-2018-4-english-2.pdf). This implementation considers the effect of including or excluding building facade geometries (e.g. balconies, balcony railings, etc.) that may obstruct daylight access in densily built urban environments. Finally, this implementation also takes into consideration how using different building facade materials and colours affects daylight access.

<br>

<ins><b>Step 1:</ins></b> Add the geometries (Geometry Pipeline) of the room (walls, ceiling, floor, windows, eaves) <br><br>
<ins><b>Step 2:</ins></b> Add the geometries (Geometry Pipeline) of the obstructions (e.g. ground, building facades of surrounding buildings, balconies of surrounding buildings, balcony railings of surrounding buildings) <br><br>
<ins><b>Step 3:</ins></b> Add a slider and a panel with the standard height value of a floor (2.79m). Include a multiplier to combine the slider and the floor height values to obtain the elevation coordinates (z-coord) of the different room-related geometries from floor to floor. <br><br>
<ins><b>Step 4:</ins></b> Add one Climate Studio *LightingMaterial* module per obstructing geometry to pick an appropriate material and colour with specific spectral properties. <br><br>
<ins><b>Step 5:</ins></b> Add one Climate Studio *LightingMaterial* module for every room-related geometry and pick an appropriate material and colour.<br><br>
<ins><b>Step 6:</ins></b> Add a Climate Studio *SceneLayer* module to construct a Scene Layer for daylight simulation, one for every geometry.<br><br>
<ins><b>Step 7:</ins></b> Add a sensor grid (using the Climate Studio *SensorGrid* module) with 0.2m resolution and placed 0.8m above a room floor surface.<br><br>
<ins><b>Step 8:</ins></b> Add a *Boolean Toggle* in combination with two *Cull Pattern* modules to control when balcony and balcony railing geometries are to be included as obstructions in the DF-computation and when not. <br><br>
<ins><b>Step 9:</ins></b> Add Climate Studio *DaylightModel* to prepare the scene for running the DF daylight simulation.<br><br>
<ins><b>Step 10:</ins></b> Add a Climate Studio *Daylight* module and select *Daylight Factor* as the chosen standard to run the corresponding daylight simulation.<br><br>
<ins><b>Step 11:</ins></b> Add a *RUN-button* to control the execution of the DF-computation. <br><br>
<ins><b>Step 12:</ins></b> <br><br>

<img src="img//DF_gh_flowchart.png"></img>

<br>
<br>


## Output:
The computed Daylight Factor for every point in the grid is stored in 

<p align="center"><img src="img//OA_tool_output.png" width=70%></img></p>

<br>
<br>


## References:
Dubois, M-C., Gentile, N., Laike, T., Bournas, I., & Alenius, M. (2019). Daylighting and lighting under a Nordic sky. (First ed.) Studentlitteratur AB. 
<br>
<br>


## License
Copyright 2023 Sustainable3DCities <br><br><br>
The 3-Clause BSD License <br>
https://opensource.org/licenses/BSD-3-Clause <br>
<br><br><br>
Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

