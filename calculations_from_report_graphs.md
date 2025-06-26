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
- Y axis - pore water pressure 
    - pore water pressure
    - mid pore water pressure if avalible
- X axis - elapsed time
- If there are more than 500 data points select every nth point where n is total / 500
### Isotrophic Consolidation IV - pwp time
- X axis - time since start of stage
- Y axis - DissipationPCT
- initial PWP = first data point in basepwpdata
- MAXpwp = MAX(base PWP)
    - only process data after MAX(pwp)
    - $$dissipationPCT = \frac{initialPWP - PWP}{initialPWP}\times 100$$
    - If there are more than 200 data points select every nth point where n is total / 200
### Isotrophic Consolidation V - vol elapsed
- X axis - time since start of stage 
- Y axis - volunm change 
- If there are more than 300 data points select every nth point where n is total / 300
### Isotrophic Consolidation VI void time
- X axis - time since start of stage 
- Y axis - current void data 
    - $$volumChange(cm^3) = initialVolum - \frac{volChange(mm^3)}{1000}$$
    - $$solidsVolumm = \frac{initialVolum}{1 + initialVoidRatio}$$
    - $$voidsVolumn = currntVolum(cm^3) - solidsVolumn$$
    - $$currentVoidRatio = \frac{voidsVolumn}{solidsVolumn}$$


## Anisotrophic consolidation plots
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

### Anisotrophic Consolidation I - axial mean effective
- X axis - effective mean stress
- Y axis - axial strain
- Caculate moving average for cutting down data 
    - $$startIDX = MAX(i - Int(\frac{windowSize}{2}))$$
    - $$endIDX = MIN(i +INT(\frac{windowSize}{2}+1))
- If there are more than 200 data points select every nth point where n is total / 200
### Anisotrophic Consolidation II - dev Cambridge
- X axis - effective cambridge p
- Y axis - deviator stress
### Anisotrophic Consolidation III - time vs s base
- Y axis - tPrime
- X axis - sPrime
    - $$tPrime = \frac{effectiveAxial - effectiveRadial}{2}$$
    - $$sPrime = \frac{effectiveAxial + effectiveRadial}{2}$$
### Anisotrophic Consolidation IV - t vs s mid
- Y axis - tPrime
- X axis - sPrime
- calculate axial stress if not avalible base on avalible data 
    - $$axialStress = cellPressure +deviatorStress$$
    - $$axialStress = effectiveAxial +midPWP$$
    - $$axialStress = \frac{axialForce}{currentArea}  $$
- calculate effective stress
    - $$effectiveAxialMid = axialStress - midPWP$$
    - $$effectiveRadialMid = cellPressure - midPWP$$
- calculate tprime and sPrime
    - $$tPrime = \frac{effectiveAxial - effectiveRadial}{2}$$
    - $$sPrime = \frac{effectiveAxial + effectiveRadial}{2}$$
### Anisotrophic Consolidation V - pwp time ani
- X axis - 
    - if : $$ \frac{MAXtime}{MINtime + 0.1}>100$$ X axis is log(time)
- Y axis -  mid and base PWP 
- If there are more than 500 data points select every nth point where n is total / 500
### Anisotrophic Consolidation VI volumetric time ani
- X axis - time since start of stage 
- Y axis - volumn change 
### Anisotrophic Consolidation VII volstrain time ani
- X axis - Time since start of stage 
- Y axis - Volumetric strain 
    - $$ volumStrain = \frac{volChange}{initialVolum}\times 100$$
    - if max change>0: $$volumStrain= \frac{volChange}{maxChange}\times 10$$


## Undrained Loading Plots
defult values:
- Initial Volum (cm^3) = 100.0
- Initial void ratio = 0.8
- $$ initialVolum = \pi \times (\frac{initialDiameter(mm)}{2})^2\times \frac{initialHeight(mm)}{1000}$$
- if temp VR >0: initial void ratio = tempVR

### Undrained Loading I axial mean effective
- X axis - mean effective stress (kPa)
    - if length(meanEffectiveStress)>1000: $$ subsampleRate = \frac{len(plotIndicies)}{1000}$$
    - select every nth value accourding to subsample rate of mean effective stress
- Y axis - axial strain (%)
    - if len(axial strain) > 100: $$markerStep=\frac{len(plotIndiciesSub)}{50}$$
    - select every nth value according to marker step of axial strain

### Undrained Loading II deviator cambridge
- X axis - Cambridge P (KPa)
    - if length of Cambridge P> 1000: $$subsample rate = \frac{length(CambridgeP)}{1000}$$
- Y axis - Deviator Stress (KPa)
    - if length of deviator stress > 100: $$subsampleRate = \frac{len(DeviatorStress)}{50}$$
### Undrained Loading III t vs s base 
- X axis - sPrime
    - $$sPrime = \frac{effectiveAxial + effectiveRadial}{2}$$
    - if Len(sPrime)> 1000: $$subsampleRate = \frac{len(sPrime)}{1000}$$
- Y axis - tPrime
    - $$tPrime = \frac{effectiveAxial - effectiveRadial}{2}$$
    - if Len(tPrime)> 1000: $$subsampleRate = \frac{len(tPrime)}{50}$$
### Undrained Loading IV t vs s mid
- Y axis - tPrime
    - if Len(tPrime)> 1000: $$subsampleRate = \frac{len(tPrime)}{50}$$
- X axis - sPrime
    - if Len(sPrime)> 1000: $$subsampleRate = \frac{len(sPrime)}{1000}$$
- calculate effective stress
    - $$effectiveRadialMid = cellPressure - midPWP$$
    - $$effectiveAxialMid = axialStress - midPWP$$
    - or: $$effectiveAxialMid = (cellP + devS) - midPWP$$
- calculate tprime and sPrime
    - $$tPrime = \frac{effectiveAxial - effectiveRadial}{2}$$
    - $$sPrime = \frac{effectiveAxial + effectiveRadial}{2}$$
### Undrained Loading V PWP time undrained 
- Y axis - PWP
- X axis - Time 
    - if Len(time)> 1000: $$subsampleRate = \frac{len(time)}{1000}$$
    - if Len(subsample rate)> 1000: $$subsampleRate = \frac{len(subsamplerate)}{50}$$

## Cyclic loading 
### Cyclic  loading table
- Calculation double amplitude
    - $$strainDA = maxStrain - minStrain$$
    - $$stressDA = maxStress - minStress$$
- calculatin Young's modulus
    - if strainad>0:  $$youngsModulus(KPa) = \frac{stressDA}{\frac{strainDA}{100}}$$
    - $$YoungsModulus(MPa) = \frac{youngsModulus(KPa)}{1000}$$
- Calculate Damping Coefficent 
    - Calculate hysteresis loop area
        - $$LoopArea = 0.5\times \sum_{i=1}^{n}(x_i \times y_{i+1} - x_{i+1} \times y_i)$$
    - strain and stress amplitudes 
        - $$strainDA = maxStrain - minStrain$$
        - $$stressDA = maxStress - minStress$$
        - $$ strainAmplitude = \frac{strainDA}{2}$$
        - $$ stressAmplitude = \frac{stressDA}{2}$$
    - Maximum stored elastic energy 
        - $$storedEnergy = 0.5 \times strainAmplitude \times StressAmplitude$$
    - Calculate damping coefficcent 
        - $$dampingRatio = \frac{loopArea}{4\times \pi \times storedEnergy}$$
        - $$dampingPercent = dampingRatio \times 100$$
        - $$dampingPercent = 0.1 < dampingPercent < 25$$
- Calculate permanent axial strain (%)
    - Check all stresses are positive and there is at least 2 data points 
    - detect when data crosses 0 and use linear interpolation to find strain where stress is 0
        - $$ \text{For each } i  \in \{1, 2, \ldots, n-1\}, \text{ if } \text{stresses}_{i-1} \times \text{stresses}_i < 0,\text{ then:}$$
        - $$ \text{Zero Crossings} = \text{strains}_{i-1}-(\frac{\text{stresses}_{i-1}}{stresses_i - stresses_{i-1}}) \times (strains_i-strains_{i-1})$$
        - permenant strain = mean(Zero Crossings)
        - else use midpoint of strains at min/max stress 
        - If permanat strain > 1.0: $$ permanentStrain = \frac{permenantStrain}{3100}$$
        - Ensure: 0.0 < permenant strain  < 1.0
### For each stage with cyclic data
- Calculate CRS
    - $$CRS = \frac{maxDeviator - minDeviator}{2\times effectiveConfiningPressure}$$
    - CRS = Max(CRS)
- Calculate average CRS
    - $$CRS = \frac{maxDeviator - minDeviator}{2\times effectiveConfiningPressure}$$
    - CRS = Average(CRS)