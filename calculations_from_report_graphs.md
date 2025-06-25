# Cyclic Triaxial Testing Calculation Validation for Plots

## Saturation Plots
### Stauration I - Time Plot
- Pressure vs Time
- X axis - Square root of time (s)
- Y axis - Pressure (kPa)
- Group data by stage
- start all data at 0
- get last value from previous stage
- Take the median of the last few values for stability
    - cellValue = median(cellValue)
    - baseValue = median(baseValue)
    - midValue = median(midValue)
    - all fallback of last value
- stagetime is 120000 if sttage number is 1 and otherwise is 100000
- cumulative time = cumulative time + stage time 
### Saturation II - Cell pressure plot
- pressure vs cell pressure 
- X axis Cell Pressure (kPa) from database
- Y Axis Pressure (kPa) from database

## Isotrophic Consolidation Plots
defult values:
- Initial Volum (cm^3) = 100.0
- Initial void ratio = 0.7
- partical density = 2.65
- Volum calculations
    - $$radius(cm) = \frac{initialDiameter(mm)}{20}$$
    - $$height(cm) = \frac{initialHeight(mm)}{10}$$
    - $$initialVolum(cm^3) = \pi \times radius(cm) \times radius(cm) \times height(cm)$$
- Dry density and void ratio
    - $$bulkDensity = \frac{initialMass(g)}{initialVolum(cm^3)}$$
    - moisture content 
    - $$moistureContent = (\frac{iniTinWet - iniTinDry}{iniTinDry - iniTinMass})\times 100$$
    - $$dryDensity = \frac{bulkDensity}{1 + \frac{moistureContent}{100}}$$
    - $$volumSoilids = \frac{dryDensity\times initialVolum}{particleDensity}$$
    - $$volumVoids = initialVolum - volumSolids$$
    - $$initialVoidRatio = \frac{volumVoids}{volumSolids}$$

### Isotrophic Consolidation I - axial log
- X axis - Log(time)
- Y axis - Axial strain from database
- If there are more than 200 data points select every nth point where n is total / 200
### Isotrophic Consolidation II - volum log
- X axis - Log(time)
- Y axis - volum strain
- Caculate volumetric strain 
    - $$volStrainPCT = (\frac{volChageFloat}{initialVolum})\times 100$$
- If there are more than 200 data points select every nth point where n is total / 200
### Isotrophic Consolidation III - pwp elapsed


### Isotrophic Consolidation IV - pwp time


### Isotrophic Consolidation V - vol elapsed


### Isotrophic Consolidation VI void time
