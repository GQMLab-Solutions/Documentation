# Cyclic Triaxial Testing Calculation Validation for Tables 

## Specimin details (line 856)
#### From database:
- specimen_height_mm 
- specimen_diameter_mm 
- specimen_mass_initial_g 
- specimen_mass_final_g 
- particle_density_mg_m3 
- ini_tin_mass
- ini_tin_wet
- ini_tin_dry
- fin_tin_mass
- fin_tin_wet
- fin_tin_dry
#### Calculations
- Specimin Volume 
    - $$Radius(cm) = \frac{specimin Diameter(mm)}{20}$$
    - $$Height(cm) = \frac{specimin Height(mm)}{10}$$
    - $$Volume(cm^3) = \pi\times radius(cm) \times radius(cm) \times height(cm)$$
- Initial Water Content %
    - $$(\frac{initialTinWet - initialTinDry}{initialTinDry - initialTinMass})\times 100$$
- Final Water Content %
    - $$(\frac{finalTinWet - finalTinDry}{finalTinDry - finalTinMass})\times 100$$
- Bulk Density Mg/m³
    - $$BulkDensity = \frac{initalSpeciminMass(g)}{volume(cm^3)}$$
- Dry Density Mg/m³
    - $$DryDensity = \frac{bulkDensity}{(1 + (\frac{initiaMoisture}{100}))}$$
- Void Ratio 
    - $$volumeSolids = \frac{dryDensity\times volume(cm^3)}{particleDensity(Mg/m^3)}
    - $$volumeVoids = volume(cm^2) - volumeSolids$$
    - $$VoidRatio = \frac{volumeVoids}{volumSolids}$$

## Saturation Table (line 1037)
#### From Database 
- b_value as Max B value
- cell_pressure
- back_pressure
- pore_pressure
- mid_plane_pore_pressure
- test_stages
- min_time
- max_time
- cell_pressure as start cell
- pore_pressure as start pore 
#### Calculations
- All data from database aside from below calculations
- B Value
    - $$deltacell = endCell - startCell$$
    - $$deltaPore = endPore - startPore$$
    - $$BValue = \frac{deltaPore}{deltaCell}$$
- effective pressure 
    - $$effectiveBasePressure = cellPressure - porePressure$$
    - $$effectiveMidPressure - cellPressure - midPlanePorePressure$$

#### Decimal placed
- B Value = 2 dp

## Isoconsolidation Table (line 1279)
#### From database 
- specimen_mass_initial_g,
- particle_density_mg_m3,
- specimen_height_mm,
- specimen_diameter_mm,
- ini_tin_mass_content,
- ini_tin_wet_content_initial,
- ini_tin_dry_content_final
- cell pressure 
- back pressure
- base pwp
- plane pore pressure as mid pwp
- current height
- current diameter 
- volum change as volume
- deviator stress
- axial stress
#### Calculations 
- Data from database all rounded to 1 dp aside from void ratio to 3dp
- Moisture content 
    - $$waterMass = wetMass - dryMass$$
    - $$soilMass = dryMass - tinMass$$
    - $$moistureContent = (\frac{waterMass}{soilMass})\times 100$$
- Initial Void Ratio
    - $$initialVolume = \pi\times (\frac{\frac{diameter(mm)}{2}}{10})^2\times(\frac{height(mm)}{10})$$
    - $$dryMass = \frac{speciminMass}{1 + \frac{moistureContent}{100}}$$
    - $$volumeSolids = \frac{dryMass}{particleDensity}$$
    - $$initialVoidRatio = \frac{initialVolume - volumeSolids}{volumeSolids}$$
- Deviator stress calculation (only used if deviator stress is not given)
    - $$deviatorStress = axialStress -cellP$$
    - 1 dp
- Effective Pressure 
    - $$effectivePBase = cellP - basePWP$$ 
    - $$effectivePMid = cellP - midPWP$$
- Void Ratio
    - $$origionalVolume(mm^3) = \pi \times (\frac{speciminDiameter}{2})^2\times speciminHeight$$
    - $$currentVolume = origionalVolume(mm^3) + volumChange$$
    - $$volumRatio = \frac{currentVolum}{originalVolum(mm^3)}$$
    - $$voidRatio = initialVoidRatio \times volumRatio$$
- Specimin Volum cm^3
    - $$area(mm^2) = \pi\times(\frac{diameter}{2})^2$$
    - $$volum(mm^3) = area(mm^3)\times height$$
    - $$speciminVolum(cm^3) = \frac{volum(mm^3)}{1000}$$
## Anisocosolidation (line 1570)
#### From database 
- specimen_mass_initial_g,
- particle_density_mg_m3,
- specimen_height_mm,
- specimen_diameter_mm,
- ini_tin_mass_content,
- ini_tin_wet_content_initial,
- ini_tin_dry_content_final
- cell pressure 
- back pressure
- base pwp
- plane pore pressure as mid pwp
- current height
- current diameter 
- volum change as volume
- deviator stress
- axial stress
#### Calculations 
- Calculations same as Isoconsolidation but using next stage 
## Undrained Loading (line 1850)
#### From database 
- specimen_mass_initial_g,
- particle_density_mg_m3,
- specimen_height_mm,
- specimen_diameter_mm,
- ini_tin_mass_content,
- ini_tin_wet_content_initial,
- ini_tin_dry_content_final
- cell pressure 
- back pressure
- base pwp
- plane pore pressure as mid pwp
- current height
- current diameter 
- volum change as volume
- deviator stress
- axial stress
## Shear (line1997)
#### From database 
- specimen_mass_initial_g,
- particle_density_mg_m3,
- specimen_height_mm,
- specimen_diameter_mm,
- ini_tin_mass_content,
- ini_tin_wet_content_initial,
- ini_tin_dry_content_final
- cell pressure 
- back pressure
- base pwp
- plane pore pressure as mid pwp
- current height
- current diameter 
- volum change as volume
- deviator stress
- axial stress

## Cyclic Loading (line 2082)
#### From database 
- specimen_mass_initial_g,
- particle_density_mg_m3,
- specimen_height_mm,
- specimen_diameter_mm,
- ini_tin_mass_content,
- ini_tin_wet_content_initial,
- ini_tin_dry_content_final
- cell pressure 
- back pressure
- base pwp
- plane pore pressure as mid pwp
- current height
- current diameter 
- volum change as volume
- deviator stress
- axial stress
#### Calculations 
- Data Querry
    - $$singleAmpStrain = \frac{Max(axialStrain) - MIN(axialStrain)}{2}$$
    - if no max cyclic stress ratio in database: 
        - $$cyclicStressRatio = \frac{MAX(deviatorStress) - MIN(deviatorStress)}{2\times MAX(cellPressure)-(backPressure)}$$
    - $$deviatorStress = MAX(deviatorStress)-MIN|(deviatorStress)$$
    - Calculate base excess pore water pressure ratio with CORRECTED order of subtraction
        - Get the maximum pore pressure in the last VALID cycle (with >= 90 rows)
        - Get the first pore pressure value for this stage
        - $$baseEPWP = MAX(cellPressure) - (porePressure from first stage(intimeorder))\times 100$$
    - Calculate mid excess pore water pressure ratio with CORRECTED order of subtraction
        -  Get the maximum mid plane pore pressure in the last VALID cycle (with >= 90 rows)
        - Get the first mid plane pore pressure value for this stage
        - $$midEPWP = MAX(cellPressure) - (porePressure from first stage(intimeorder))\times 100$$
    - $$compExtRatio = \frac{MAX(deviatorStress)-55}{MIN(deviatorStress)-55}$$
    - Update permanent axial strain to use the last valid cycle with 90+ rows
    - Values formatted to 2 dp
