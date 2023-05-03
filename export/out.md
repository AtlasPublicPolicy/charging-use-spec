<div align="center">
<img src="https://evchargingspec.org/wp-content/uploads/2022/05/evcu_github.png" alt="EV Charging Use Data Specification logo"/>
 </div>
 
 # About
The Electric Vehicle Charging Use Data Specification (specification) defines a common format and process for provisioning, collecting, validating and reporting on data related to electric vehicle (EV) charger deployment and use. 

Government and utility funded EV charging station deployment programs are expanding rapidly. Evaluation, measurement and verification of the performance of these public and utility programs requires substantial data collection and processing efforts. A common specification for these data which standardizes input data, processing, and outputs can improve the efficiency and effectiveness of public or ratepayer funded charging programs. Common data reporting requirements across funding programs can reduce compliance burdens for obligated parties. 

# Specification Overview
The specification is flexible and extensible depending on program specifics and evaluation measurement and verification requirements of the funding organization. It is organized into the core specification which details data collection fields, data validations, and reporting outputs for basic tracking, evaluation and verification uses. The specification also supports  extensions that enable additional reporting functionality.

Refer to the [glossary](glossary.md) for definitions of specific termination used in this specification and an outline of the [roles and responsibilities](glossary.md#specification-roles) of the entities involved in the data reporting process. The [field type and format definitions](field-type-and-format-reference.md) reference defines the data types and formats expected in data collection fields.

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

 2. Participate in a meeting. [Atlas Public Policy](https://atlaspolicy.com) has served as the primary convener of parties interested in contributing to the specification and hosts open meetings. All meetings are recorded and can be watched later. Past and upcoming meetings are available on [evchargingspec.org](https://evchargingspec.org). 

 3. Send an email to info@evchargingspec.org with any questions or feedback. All emails sent to this address related to the specification will be published on GitHub. Please indicate in your email if you would like attribution or if you would like to remain anonymous. This email is monitored by staff at [Atlas Public Policy](https://atlaspolicy.com).

See the [specification roadmap](roadmap.md) for upcoming work on the specification including new components and other related work.  

*The content of this specification is [licensed](LICENSE) under [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)*
# Field Type Definitions
Refer to these field type definitions for data collection formats.
- **Charger Type** - Standard charger type – One of the following: L1, L2, DCFC
- **Connector Type** - Standard connector type – One of the following: J1772, CHAdeMO, Tesla, CCS, CCS/CHAdeMO, CCS/Tesla, CHAdeMO/Tesla, CHAdeMO/CCS/Tesla
 - **Currency** - Currency is a specialized numeric field that contains exactly two significant digits.  *Example: 5.00 but not 5.000 or 5*
 - **Date/time** - string field with the format: YYYYMMDD hh:mm:ss [+/-hh:mm] where time is represented by a 24 hour clock and time in brackets represents the distance from coordinated universal time.  *Example: 20220101 01:01:01 [-5:00] represents January 1, 2022 at 12:01 AM ET*
 - **Duration** - string field with the format HH:MM:SS used to encode elapsed time. *Example: 01:30:00 for 1 hour and thirty minutes*
 - **Email** - properly formatted email address. *Example: example<void>@example.com*
 - **Float** - numeric field that may contain up to seven significant digits. *Example: 1.111 or 1.1111111*
 - **ID** - sequence of UTF-8 characters. ID fields labeled unique must be unique to the conditions described in the field description. ID fields that are labeled foreign reference ID fields in other tables.
 - **Integer** - specific numeric fields which may only contain whole numbers. *Example: 2 or 5 but not 2.1*
 - **Latitude** - WGS84 latitude in decimal degrees to at least 4 decimal places ([EPSG:4326](https://epsg.io/4326)). Must be between -90.0 and 90.0. *Example: 38.8894 for the Washington Monument*
 - **Longitude** - WGS84 longitude in decimal degrees to at least 4 decimal places ([EPSG:4326](https://epsg.io/4326)). Must be between -180.0 and 180.0.  *Example: -77.0352 for the Washington Monument*
 - **Numeric** - A numeric field contains only properly formatted numbers. Empty numeric fields are \<NA>. *Example: 10 or 99 but not 099*
 - **String** - Text field of UTF-8 characters (letters, numbers, punctuation, and symbols). Empty string fields are \<NULL>.
 - **TRUE/FALSE** - Boolean value symbolized by text “TRUE” or “FALSE”
 - **ZIP Code** - valid five-digit ZIP code between 00501 and 99950. *Example: 20500 for the White House*
# Core Specification
The core specification detailes data collection fields, data validations, and reporting outputs for basic tracking, evaluation and verification uses. 

 - [Registration and Session Data Collection Reference](registration-and-session-data-reference.md) - Format and process for registering participant organizations and funded charging stations and collecting session-level usage data.
 - [Validation Reference](validation-reference.md) - Validation procedures and parameters for registrations and session use data.
 - [Reporting Metrics Reference](reporting-metrics-reference.md) - Common reporting metrics supported by the specification.
# Data Validation

This section describes the individual validations to be performed on the registration and session data that ensure that they conform to specifications and that measurements fall within expected parameters. Data received by the data aggregator may have quality issues caused by measurement or data processing errors that interfere with successful data ingestion or the calculation of valid reporting metrics.

The data validation process performs a series of automated checks on the received data, flagging it as erroneous or non-compliant if such checks fail. Data that passes all validation checks will be considered validated data, meaning that the data aggregator has identified it as compliant with the charging use data specification and certified its use in reporting.

Validations for data fields return one of three results:

![](https://via.placeholder.com/15/09692e/000000?text=+)**Valid** – entry conforms to expected type, format, and parameters   
![](https://via.placeholder.com/15/ffc800/000000?text=+)**Warning** – entry exceeds parameter(s) range and requires manual quality assurance check  
![](https://via.placeholder.com/15/c40404/000000?text=+)**Error** – required data missing or not conformant to expected type, format, or parameters  

[Warnings](#warning-validations) result from:
- Measurement parameter validation failures specified in the [Warnings Validations](#warning-validations) section of this document.
- Duplication validation failures.

[Errors](#error-validations) result from:
- Nonconformity with field type and format as specified in the [Field Type and Format Reference](../field-type-and-format-reference.md).
- Missing data specified as required data in the [Field Type and Format Reference](../field-type-and-format-reference.md).
- Select parameter validation failures described in the [Error Validations](#error-validations) section of this document.

## Warning Validations
Measurements that fall outside of designated ranges may indicate potential measurement errors, errors from faulty processing/record keeping, or other causes of invalid data. Because these validation failures may trigger on edge-case measurements that are nonetheless valid, they should be checked manually for possible exclusion from reporting metric calculations.

Duplication of unique ID fields might indicate duplicate records but might also indicate that the ID field has been assigned to a record erroneously. Duplicate records can usually be safely excluded, but other cases require additional attention.

The tables in this section outline the field validation types and parameters that result in a warning flag for registration and session data.

**Table 1. Registration Data Warning Validations**

| **Name** | **Field(s)** | **Type** | **Description and Parameters** |
| --- | --- | --- | --- |
| **Duplicate Project ID** | project\_id | duplicate | The project\_id value already exists in registration data. |
| **Duplicate Site ID** | site\_id | duplicate | The site\_id value already exists in registration data. |
| **Duplicate Site Address** | address\_1<br /> address\_2<br />  city <br />state <br />  zip\_code | duplicate | The combination of site address field values already exists in registration data. |
| **Duplicate Station ID** | station\_id | duplicate | The station\_id value already exists in registration data. |
| **Power Rating Out of Range** | power\_level\_kw <br />connector\_type | consistency  range | The power\_level\_kw value is within range consistent with station type. Recommended ranges are: 3.2kW – 19.2kW for L2 connectors and 20kW – 360kW for DCFC connectors. |

**Table 2. Session Data Warning Validations**

| **Name** | **Field(s)** | **Type** | **Description and Parameters** |
| --- | --- | --- | --- |
| **Short Session Duration** | session\_duration <br />charging\_duration | constraint | The session\_duration or charging\_duration values are less than program defined short duration parameters. Recommended parameter is one minute. |
| **Excess Session Duration** | session\_duration <br />charging\_duration | constraint | The session\_duration or charging\_duration values are greater than program defined excess session length parameters. Recommended parameters are 2,880 minutes (two days) for session\_duration and 1440 minutes (one day) for charging duration. |
| **Low Energy Delivered** | energy\_kwh | constraint | The energy\_kwh value is less than program-defined low energy parameters. Recommended parameter is 0.5 kWh. |
| **Excess Energy Delivered** | energy\_kwh | constraint | The energy\_kwh value is greater than program-defined excess energy parameters. Recommended parameter no more than 250 kWh. |
| **Charging Exceeds Session Duration** | charging\_duration<br />session\_duration | consistency | The charging\_duration value is greater than the session\_duration value. |
| **Session Power Above Rating** | energy\_kwh <br />charging\_duration <br />power\_level\_kw | consistency | The average power delivered (energy\_kwh / [charging\_duration / 60]) is more than 10% higher than rated power (power\_level\_kw \* 1.1). |

## Error Validations

Records flagged with an error should be excluded from the reporting data and referred back to the Data Provider for possible correction. The tables in this section outline the field validation types and parameters that result in an error flag for session data.

**Table 3. Registration Data Error Validations**

| **Name** | **Field(s)** | **Type** | **Description and Parameters** |
| --- | --- | --- | --- |
| **Invalid Geography** | city<br />state<br />zip\_code<br />latitude<br />longitude | cross reference | The station/site geographic identifiers fall outside of the range of the program geography. E.g. zip\_code does not match master list of eligible Zip codes or lat/lon fall outside program area (or bounding box). |
| **Activation Date Out of Bounds** | station\_activation\_date <br />project\_award\_date | consistency cross reference | The station\_activation\_date and/or project\_award\_date fall after the reportinging period or before the program start date. |
| **No Onsite Generation Parameters** | onsite\_generation <br />onsite\_generation\_type <br />onsite\_generation\_power | consistency cross reference | The onsite\_generation\_type and onsite\_generation\_power fields are not NULL if onsite\_generation field is TRUE. |
| **No Onsite Storage Parameters** | onsite\_storage <br />onsite\_storage\_energy <br />onsite\_storage\_power | consistency cross reference | The <br />onsite\_storage\_energy and onsite\_storage\_power fields are not NULL if onsite\_storage field is TRUE. |

**Table 4. Session Data Error Validations**

| **Name** | **Field(s)** | **Type** | **Description and Parameters** |
| --- | --- | --- | --- |
| **Date Outside Reporting Period** | plug\_start\_datetime<br />charge\_start\_datetime | consistency | The plug\_start\_datetime or charge\_start\_datetime values do not fall within the date range of the reporting period. |
| **No Matching Registration** | station\_id | cross reference | The session station\_id is not in the program station registry. |
| **Zero Length Session Duration** | session\_duration<br />charging\_duration | constraint | The session\_duration or charging\_duration values are zero. |
| **Zero Energy Session** | energy\_kwh | constraint | The energy\_kwh value is zero. |
# Supplementary Materials

1. [Data Integration Support](data-integration-support.md)
2. [Example Program Language](example-program-language.md)
# Data Integration Support

The EV Charging Use Data Specification is meant to provide a pathway for industry and regulators to develop a common method by which to track charging use data that increases usability of the data and reduces effort for all involved. However, because these data are currently collected and stored in a fragmented and ad hoc way, challenges are likely in the transition process, especially as this specification is implemented in places where legacy reporting processes are already in place.

This reference documents common data quality and conformity issues encountered in past EV charging use data collection efforts and provides methods to address those issues to create specification compliant data. It is presented here as guidance for Data Providers and Program Administrators to handle conversions from internal or legacy data formats to specification-ready data, or for Data Aggregators that encounter out-of-specification data submitted by Data Providers or Program Administrators.

## Contents

1. [General Transformations](#general-transformations)
2. [Registration Data](#registration-data)
3. [Session Data](#session-data)

## General transformations
To transform non-conformant source data to a specification-ready format the following general steps should be followed

- Rename alternatively-named fields to specification-standard field names if field values are consistent.
- Type-define fields and ensure that empty fields are either NULL (if numeric) or NA (if string).
- Assign fields to appropriate project, site, or station table if provided in same table in source data
- Append fragmented records into single project, site, station, or session tables

## Registration Data

Registration data is often entered manually using software that does not allow for robust entry checking and is therefore prone to error. Furthermore, registration data may be sourced from program information that was not expressly collected to build a station registry for reporting purposes and therefore might differ substantially from the fields defined in the specification.

Common issues with missing, incomplete, or incompatible fields and solutions/workarounds for those issues are described in the table below.

**Table 1. Common Registry Data Quality Issues**

| Issue | Field(s) | Solution/Transformation |
| --- | --- | --- |
| Missing, incomplete, or erroneous station\_id field. | station\_id |The station identifier is a critical link between registration data and session data without which, most reporting is impossible. If station\_id is missing, incomplete or incorrectly entered in the source data, it may be possible to link registration data to session data using the station\_serial field (if provided) and the network name. Once linked, the station\_id field may be back-filledbackfilled into the registration data using a lookup table based on session reporting.<br /><br />If no match is found, it may be possible to work with the program administrator and/or the data provider to create an override table that replaces or fills in corrected station\_id using station serial numbers.|
| No charging site registration | site\_id | If source data do not include a site registration structure but station addresses are reported, the site registration table can be constructed by grouping stations by common address fields. A site\_id may be generated for each unique address and any site\_id attributes reported at the station level may be promoted to the charging site registration table. |
| Connector type does not match formatting for _connector_ in the data types and formats reference | connector\_type | If connector type is reported in the source data in a consistent way then a lookup table can be used to crosswalk the non-standard entries to standard values. If connector type is not reported consistently, then manual correction may be required. |

## Session Data

Individual data providers have unique internal data structures in which they store and report on charging sessions. Due to this fragmentation, session data sourced from data providers internal databases or data sharing portals may require substantial modification in order to comply with the specification.

The table below details common issues with missing, incomplete, or incompatible fields and solutions/transformations that can be used to conform session source data with the specification.

**Table 2. Common Session Data Quality Issues**

| **Issue** | **Field(s)** | **Solution/Transformation** |
| --- | --- | --- |
| **Session data records missing identifier** | session\_id | If source data does not provide a session id, and session\_id is not required to link session data to extended usage data such as electric grid impact (intervals), a unique identifier may be generated and assigned to each session after a duplicate check that ensures that no duplicate session records exist in the dataset. |
| **Station identifier missing** | station\_id | The station identifier is a critical link between session data and registry data. If station\_id is not available in the source data, session data may be linked to station registration table using the station\_serial field (if provided) and the network name. Once linked, the station\_id field can be back-filled from the registration record. <br /> <br /> If no match is found, further information is required from the data provider or program administrator to successfully match session data to station.|
| **Missing port number** | port\_number |If port\_number is unavailable in the source data and the associated station is a single-port station, port\_number is assigned to 1. <br /> <br /> If the associated station is a multi-port station, then further information is required from the data provider. |
| **Non-standard or separated date/time field(s)** | plug\_start\_datetime | If a full datetime value is provided in the source data in a non-standard format, it should converted to the specified date/time format. <br /> <br />If date and time are provided separately, they should be combined in the specified data/time format. Where a time zone is not indicated, assume time is localized to station location. |
| **Non-standard or missing session duration or charging duration** | session\_duration | If session duration or charging duration are reported in a non-standard format, reformat to specified format with as much precision is possible given duration input. <br /> <br />If no session\_duration is available in the source data, but a plug\_end\_datetime is provided, session\_duration can be calculated as plug\_end\_datetime minus plug\_start\_datetime. <br /> <br /> If charging\_duration is not available but time idle is reported in the source data, charging\_duration can be calculated as session\_duration minus idle\_time. |
| **Session energy reported in unit other than kWh** | energy\_kwh | If session energy delivery is reported in a way that indicates use of an energy unit other than kWh, then that field can be converted to energy\_kwh using standard conversion factors (e.g. energy reported in MWh can be converted to kWh by multiplying MWh by 1,000). |
| **Session peak power reported in unit other than kW** | peak\_kw | If session peak power is reported in a way that indicates use of an energy unit other than kW, then that field can be converted to peak\_kw using standard conversion factors (e.g. energy reported in MW can be converted to kW by multiplying MW by 1,000). |

# Example Program Language

This section is intended to provide example language to include in program documentation for participants to provide clarity on the use of data being collected. The example documentation was adapted from program documentation for the [PON 4743](https://portal.nyserda.ny.gov/servlet/servlet.FileDownload?file=00Pt000000aumUtEAI) from the New York State Energy Research and Development Authority.

Below are terms that are specific to the program.

- [DELIVERABLE]: These includes report or other deliverables related to the program.
- [ENTITY]: This is intended to be the public or private entity that is administering the program.
- [STATEMENT OF WORK]: The main statement of work for program.

The below text is available in binary format for use in word processing applications here: [example-program-language.odt](https://github.com/AtlasPublicPolicy/charging-use-spec/raw/main/supplementary-materials/example-program-language.odt)

## Definitions

**Contract Information** : Recorded information regardless of form or characteristic first produced in the performance of this Agreement, that is specified to be compiled under this Agreement, specified to be delivered under this Agreement, or that is actually delivered in connection with this Agreement, and including the [DELIVERABLE] delivered by Contractor pursuant to [STATEMENT OF WORK], if applicable.

**Proprietary Information** : Recorded information regardless of form or characteristic, produced or developed outside the scope of this Agreement and without [ENTITY] financial support, provided that such information is not generally known or available from other sources without obligation concerning their confidentiality; has not been made available by the owner to others without obligation concerning its confidentiality; and is not already available to [ENTITY] without obligation concerning its confidentiality. Under no circumstances shall any information included in the [DELIVERABLE] delivered by Contractor pursuant to [STATEMENT OF WORK], if applicable, be considered Proprietary Information.

## Rights in Information; Confidentiality

[ENTITY] shall have the right to use, duplicate, or disclose Contract Information, in whole or in part, in any manner and for any purpose whatsoever, and to permit others to do so.

The Contractor shall have the right to use Contract Information for its private purposes, subject to the provisions of this Agreement.

[ENTITY] shall have no rights to any Proprietary Information.

No information shall be treated by [ENTITY] as confidential unless such information is clearly so marked by Contractor at the time it is disclosed to [ENTITY]. Under no circumstances shall any information included in the [DELIVERABLE] delivered by Contractor pursuant to [STATEMENT OF WORK] be considered confidential or Proprietary Information.

The Contractor agrees that to the extent it receives or is given any information from [ENTITY] or a [ENTITY] contractor or subcontractor, the Contractor shall treat such data in accordance with any restrictive legend contained thereon or instructions given by [ENTITY], unless another use is specifically authorized by prior written approval of the [ENTITY] Project Manager. Contractor acknowledges that in the performance of the [STATEMENT OF WORK] under this Agreement, Contractor may come into possession of personal information. Contractor agrees not to disclose any such information without the consent of [ENTITY].

In conjunction with Contractor&#39;s performance of the [STATEMENT OF WORK], [ENTITY] or other entities may furnish Contractor with information concerning the [STATEMENT OF WORK] that is collected and stored by, or on behalf of, [ENTITY] (the &quot;Information&quot;).

Any non-public, confidential, or proprietary Information will be kept confidential and will not, without [ENTITY]&#39;s prior written consent, be disclosed by Contractor, Contractor&#39;s agents, employees, contractors or professional advisors, in any manner whatsoever, in whole or in part, and will not be used by Contractor, Contractor&#39;s agents, employees, contractors or professional advisors other than in connection with the [STATEMENT OF WORK]. Contractor agrees to transmit the Information only to Contractor&#39;s agents, employees, contractors and professional advisors who need to know the Information for that purpose and who are informed by Contractor of the confidential nature of the Information and who will agree in writing to be bound by the terms and conditions of this Agreement.

Contractor will keep a record of the location of the Information. At the conclusion of the Project Period, Contractor will return to [ENTITY] all the Information and/or provide proof to [ENTITY] that the Information was destroyed. Contractor also agrees to submit to an audit of its data security/destruction practices by [ENTITY] or its representative during the contract term and for up to two (2) years following the expiration of the Agreement.

If, in the course of performance of the Agreement, Contractor or Subcontractors (if any) encounter any information in [ENTITY] database platforms that a reasonable person would identify as unrelated to the Agreement or otherwise inadvertently produced to Contractor or Subcontractors, Contractor shall notify [ENTITY] immediately and neither Contractor nor Subcontractor shall use such inadvertently produced information for its own use. Any Contractor access to [ENTITY] information shall be used solely for [ENTITY]-related matters.