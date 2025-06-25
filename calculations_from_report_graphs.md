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


