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
