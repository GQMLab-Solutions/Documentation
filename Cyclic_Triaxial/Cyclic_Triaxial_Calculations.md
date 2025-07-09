# Cyclic Triaxial Testing PDF Report and UI Generator Outline

## Specimen Details Section on the UI

### Water Content Determination - Moisture Content as percentage (for both, initial and final):

- [ ] **Equation Verified**: Water Content Calculation
  - **Verified by**: @username
  - **Date**: 09/07/2025
  - **Implementation**: `waterContent = ((tinWetSoil - tinDrySoil) / (tinDrySoil - tinMass)) * 100`
  - **Test Status**: 
    - [ ] Formula mathematically correct
    - [ ] Implementation matches formula  
    - [ ] Edge cases tested (division by zero, negative values)
    - [ ] Unit tests passing
    - [ ] Integration tests passing
  - **Notes**: 

$$\text{Water Content} = \frac{\text{tinWetSoil} - \text{tinDrySoil}}{\text{tinDrySoil} - \text{tinMass}} \times 100$$

where:
- tinWetSoil = mass of tin + wet soil
- tinDrySoil = mass of tin + dry soil   
- tinMass = mass of empty tin

**Status**: ⏳ Pending verification