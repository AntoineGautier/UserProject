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

## FAQ

> Where in the software pipeline this is generated? From ctrl-flow, or from ctrl-flow output file(s)?

In the flow diagram at https://github.com/lbl-srg/ctrl-flow-dev/blob/main/docs/linkage-schema.md#overview-of-data-flow, this package represents the output from the "Write Selections to Modelica" routine. It is directly created from "Linkage Schema (Selections)".

> Does back translation work?

No. Instead, ctrl-flow relies on user storage (cloud-based or local) ***in its own proprietary format*** for continued editing. Once you export to a Modelica package and make changes to that exported code, you cannot import those changes back into ctrl-flow for further editing.

This limitation is due to a significant deviation of the development from the original specification at https://github.com/lbl-srg/ctrl-flow-dev/blob/main/specification/requirements.html.
That specification has been updated in [requirements.md](requirements.md) to reflect the current state of development of MBL templates and of ctrl-flow.

> Where is project meta data, such as name and address of building, stored?

This data is stored in `UserProject.Data.AllSystems`.
The current definition of the parent class `Buildings.Templates.Data.AllSystems` only includes parameters for the unit system, ventilation standard and climate zone.
We should add there the additional parameters needed to fully specify a design project.

> Where does weather data come from as nearest location may need to be pulled from server.

Nice feature to consider.

> Should entries such as `damOut(dp_nominal={15, 15})` rather use `each dp_nominal=15`? In particular if there are 50+ VAV boxes.

Nice feature to consider.
