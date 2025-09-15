# UserProject - Modelica Package Mockup

## Purpose

This is a mockup of the Modelica package that should be exported by ctrl-flow when the export functionality is developed.

## Package Structure

This package demonstrates the expected structure of what the Modelica export feature should generate:

- **AirHandlersFans/**: Air handling and fan models
  - Contains two specified configurations for VAV AHUs.
- **ZoneEquipment/**: Zone-level HVAC equipment models
  - Contains a single specified configuration for VAV boxes with reheat.
- **(AirHandlersFans | ZoneEquipment)/Configuration/**: Data records with configuration parameters, one for each configuration
  - All parameter bindings are ***literal assignments***: expressions must be pre-evaluated to their numeric/string values before export.
  - These records only contain a subset of all the parameters that define a system configuration and which are exposed in ctrl-flow.
  - This subset is the one needed to enable/disable the control parameters and equipment characteristics in **Data/**.
- **Data/**: Data records with control parameters and equipment characteristics
  - These should be mapped to the schedule pages in ctrl-flow.
  - In this example, parameters are provided for two VAV AHUs (one with each configuration) and 10 VAV boxes (all with the same configuration).
- **Examples/**: Example models demonstrating how the configured classes can be instantiated to build a simulation model.

## Dependencies

See the `uses` annotation in `./package.mo`: `Buildings(version="13.0.0")`
