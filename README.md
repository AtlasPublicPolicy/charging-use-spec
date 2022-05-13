<div align="center">
<img src="https://evchargingspec.org/wp-content/uploads/2022/05/evcu_github.png" alt="EV Charging Use Data Specification logo"/>
 </div>
 
 # About
The Electric Vehicle Charging Use Data Specification (specification) defines a common format and process for provisioning, collecting, validating and reporting on data related to electric vehicle (EV) charger deployment and use. 

Government and utility funded EV charging station deployment programs are expanding rapidly. Evaluation, measurement and verification of the performance of these public and utility programs requires substantial data collection and processing efforts. A common specification for these data which standardizes input data, processing, and outputs can improve the efficiency and effectiveness of public or ratepayer funded charging programs. Common data reporting requirements across funding programs can reduce compliance burdens for obligated parties. 

# Specification Overview
The specification is flexible and extensible depending on program specifics and evaluation measurement and verification requirements of the funding organization. It is organized into the core specification which detailes data collection fields, data validations, and reporting outputs for basic tracking, evaluation and verification uses. The specification also supports  extensions that enable additional reporting functionality.

Refer to the [glossary](glossary.md) for definitions of specific termination used in this specification. The [field type and format definitions](field-type-and-format-reference.md) reference defines the data types and formats expected in data collection fields.

## Core Specification
 - [Registration and Session Data Collection Reference](core-specification/registration-and-session-data-reference.md) - Format and process for registering participant organizations and funded charging stations and collecting session-level usage data.
 - [Validation Reference](core-specification/validation-reference.md) - Validation procedures and parameters for registrations and session use data.
 - [Reporting Metrics Reference](core-specification/reporting-metrics-reference.md) - Common reporting metrics supported by the specification.

## Specification Extensions

 - Costs data collection [\[FORTHCOMING\]](roadmap.md) — details data collection fields for funding recipient equipment and installation costs.
 - Station reliability [\[FORTHCOMING\]](roadmap.md) — details data collection and procedures for measuring station reliability.
 - Grid impacts [\[FORTHCOMING\]](roadmap.md) — details data collection and procedures for measuring station usage impact on the electricity grid.

# Supplementary Materials

 - [Data Integration Support](supplementary-materials/data-integration-support.md) provides guidance on how to translate out-of-specification registration and usage data into specification-compliant format.
 - [Example Program Language](supplementary-materials/example-program-language.md) for data collection and provisioning requirements set by funding organizations.
 - Example data files for each of the data collection field specifications. [\[FORTHCOMING\]](roadmap.md)

 
# Get Help
Questions about the specification can be directed to info@evchargingspec.org. You can also pose any questions on the [GitHub discussion forum](https://github.com/AtlasPublicPolicy/charging-use-spec/discussions). 

# Get Involved 
We welcome contributions from anyone on the specification. You can contribute directly to the specification development process in a number of ways: 
 
 1. Join a public conversation on the [GitHub discussion forum](https://github.com/AtlasPublicPolicy/charging-use-spec/discussions). 

 2. Participate in a meeting. [Atlas Public Policy](https://atlaspolicy.com) has served as the primary convener of parties interested in contributing to the EVCU specification and hosts open meetings. All meetings are recorded and can be watched later. Past and upcoming meetings are available on [evchargingspec.com](https://evchargingspec.com). 

 3. Send an email to info@evchargingspec.org with any questions or feedback. All emails sent to this address related to the specification will be published on GitHub. Please indicate in your email if you would like attribution or if you would like to remain anonymous. This email is monitored by staff at [Atlas Public Policy](https://atlaspolicy.com).

See the [specification roadmap](roadmap.md) for upcoming work on the specification including new components and other related work.  

*The content of this specification is [licensed](LICENSE) under [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)*
