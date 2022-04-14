
# Core Registration and Session Data Collection Reference
This document outlines the process, structure, and format for: 1) registering projects, and associated, sites, stations, and ports, and 2) collecting core station in-use (session) data. These data are then validated  [\[FORTHCOMING\]](roadmap.md) and transformed [\[FORTHCOMING\]](roadmap.md) with the resulting information compiled into standard reporting metrics [\[FORTHCOMING\]](roadmap.md)

Registration information is also used in specification extensions linking to cost [\[FORTHCOMING\]](roadmap.md), reliability [\[FORTHCOMING\]](roadmap.md), and grid impact [\[FORTHCOMING\]](roadmap.md) reporting specifications.

## Contents

 1. [Program Registry and Onboarding Process](#program-registry-and-onboarding-process)
     1. [Project Registration](#project-registration)
     2. [Site Registration](#site-registration)
     3. [Station and Port Registration](#station-and-port-registration)
 2. [Session Data Collection](#session-data-collection)

#  Program Registry and Onboarding Process

The program registry contains entries for all charging stations deployed by program funding and is a critical component of the evaluation, measurement, and verification process because it contains the reference information required for program reporting activities. Project registration data is collected and maintained by the [program administrator](global-reference.md) or [data aggregator](global-reference.md). Recommended practice is to integrate administrative onboarding processes with registration data collection to reduce duplicative effort and ensure that all necessary registration data collection occurs prior to funding disbursement. Figure 1 shows the program registry hierarchy with individual identifying keys that link the entries together.

**Figure 1. Registration Hierarchy**
```mermaid 
graph TD

A[Table 1: Project]
B[Table 2: Site]
C[Table 3: Station]
D[Table 4: Port]
A --site_id--> B
A --project_id--> C
B --site_id--> C
C --station_id --> D
 ```

Project registration is tied to a single [obligated party](global-reference.md) and records project-level information such as funding source and amounts. Projects are limited to a single physical address but may cover many individual charging station deployments. Site registration (based on address) is recorded in parallel with project onboarding. While a project is limited to a single site, a site may receive funding from multiple projects over time. If a second project is applied to a site that is already in the system, then it should be linked to the existing site rather than generating a new site entry.

Because charging stations generate usage data, they are the fundamental reporting unit in the program registry. Each charging station is associated with individual ports which are stored as entries in the port registry. Sessions and other usage data are linked to station/port pairs which inherit all above attributes, making it possible to link each session to the associated site, project, and [obligated party](global-reference.md). In many cases, the [obligated party](global-reference.md) will not be the organization that directly collects charging use data. Instead, many obligated parties will deploy chargers managed by a third party that monitors station usage. 

To facilitate efficient data sharing, the third party that monitors station usage may also be designated as the [data provider](global-reference.md), which allows for direct data transfer to the [data aggregator](global-reference.md) and may also provide efficiencies of scale if the third-party [data provider](global-reference.md) is contracted with multiple obligated parties. In this case, the participant must provide the [program administrator](global-reference.md) with station identifiers that are consistent with those used by the [data provider](global-reference.md) as well as the necessary credentials and information to access reported usage data. See model language for data collection [\[FORTHCOMING\]](roadmap.md) for sample language to facilitate efficient collection of data.

*Fields marked as required must be included to comply with the specification, while optional fields may be made required at the discretion of the [program administrator](global-reference.md).* 

## Project Registration
During project onboarding the [program administrator](global-reference.md) will collect and record project-level information from the applicant [obligated party](global-reference.md) as outlined in Table 1. Project registration includes applicant information and general information on project funding including public/utility funding source and amount, and must be associated with a single geographic location (site). If detailed cost information, including itemized installation costs are desired, please see the installation costs extension [\[FORTHCOMING\]](roadmap.md). 

Refer to the [field type definitions](global-reference.md) in the global reference for more information on field types. *Additional fields may be appended as new columns are needed, but existing columns and their formats should be maintained to support interoperability.*

**Table 1: Project Registration**

| Field | Description | Field Type | Required |
| --- | --- | --- | --- |
| **project\_id** | unique identity specific project | Data ID (unique) | yes |
|**site\_id** |unique identity specific to the address-specific site |ID (foreign) |yes |
| **org\_name** | organization name of the [obligated party](global-reference.md) (i.e. Acme Industries) | string | yes |
| **poc\_email** | [obligated party](global-reference.md) point of contact email address | email | yes |
| **poc\_first\_name** | [obligated party](global-reference.md) point of contact first name | string | yes |
| **poc\_last\_name** | [obligated party](global-reference.md) point of contact last name | string | yes |
|**primary\_funding\_source** |primary public funding source for the project/application | string |yes |
|**primary\_funding\_type** |primary public funding source for the project/application | string |yes |
|**primary\_funding** |amount of funding station received from the primary funding source dedicated to the charging site (can include funds for installation, e.g., make-ready, equipment, and site preparation, but should not include any funding for station operation) |currency (USD) |yes |
|**utility\_makeready** |amount of funding the project received from electric utilities dedicated to infrastructure make-ready |currency (USD) |no |
|**utility\_funding\_other** |amount of funding the project received from utility for equipment or other non-make-ready costs (should not include any funding for operational costs) |currency (USD) |no  |
|**other\_makeready** |amount of other public funding station received dedicated to infrastructure make-ready |currency (USD) |no |
|**other\_funding\_other** |amount of other public funding project received for equipment or other non-make-ready costs (should not include any funding for operational costs) |currency (USD) |no  |
|**cost\_share** |funding amount project has received from other (private, non-utility) sources when combined with primary\_funding and utility\_funding and other\_public\_funding equals the total cost of the charging installation |currency (USD) |no |
|**in\_dac** |project is located inside of disadvantaged community as defined by local jurisdiction |TRUE/FALSE |no |
|**dac\_proximate** |project is located within 0.5 miles of disadvantaged community as defined by local jurisdiction |TRUE/FALSE |no |

## Site Registration
Also during project onboarding, the [program administrator](global-reference.md) will collect site information from the applicant [obligated party](global-reference.md). If the site address of the project matches a site already in the site registry, then the project should be associated with the existing site_id.

**Table 2: Site Registration**

|**Field** |**Description** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**site\_id** |unique identity specific to the site, must be consistent across reporting periods |ID (unique) |yes |
|**site\_name** |descriptive name of charging site (e.g., Mercy Hospital) |string |yes |
|**address\_1** |site street address line one (e.g. 1600 Pennsylvania Ave NW) |string |yes |
|**address\_2** |site address line two, (e.g. Unit 1) |string |no |
|**city** |site city |string |yes |
|**state** |site state (full name) |string |yes |
|**zip\_code** |site ZIP code |ZIP code |yes |
|**operating\_status** |Operational status of station (Active or Inactive) at time of inventory  |string |yes |
|**access\_type** |Type of access available (public/unrestricted, private/restricted) |string |yes |
|**site\_type** |type of site host for the charging site. |string |yes |
|**host\_first\_name** |location site host point of contact first name |string |yes |
|**host\_last\_name** |location site host point of contact last name |string |yes |
|**host\_email** |location site host point of contact email address |email |yes |
|**county** |site county (or county analogue) |ZIP code |no |
|**site\_type\_detail** |additional detail on site host land use |string |no |


## Station and Port Registration
Also during project onboarding, the [program administrator](global-reference.md) will collect station and port information from the applicant [obligated party](global-reference.md). If usage data will be provided by a third-party [data provider](global-reference.md), collecting the station identifier used by that third party to identify specific stations in their system is a critical step in the onboarding process. This ensures that the [data aggregator](global-reference.md) can successfully link usage data secured from the [data provider](global-reference.md) to stations within the registry. The [program administrator](global-reference.md) should also have a process in place to update the station registration in the event that station is upgraded, taken offline, or if the [data provider](global-reference.md) is replaced.

Each  station inherits the attributes of the site where it is located and the project that funded it. Station registration entries also include attributes specific to the individual charging station including exact location, power level, and other station-level attributes as listed in Table 3. 

Refer to the [field type definitions](global-reference.md) in the global reference for more information on field types. * Additional fields may be appended as new columns as needed, but existing columns and their formats should be maintained to support interoperability.*

 **Table 3: Station Registration**


| **Field**   | **Definition** | **Data Format** | **Required** |
| --- | --- | --- | --- |
| **station\_id** | unique identifier of charging station - must match the [data provider](global-reference.md) ID for the station if managed by a third party [data provider](global-reference.md) | ID (unique) | yes |
| **project\_id** | project identifier | Data ID (foreign) | yes |
| **site\_id** | location identifier | ID (foreign) | yes |
| **date\_entered** | date when entry was created | date | yes |
| **station\_serial** | unique identifier of charging station derived from station serial number or network identifier (e.g., 123-345-2) | ID (unique) | yes |
| **station\_name** | name of charging station (e.g., Mercy Hospital – 2) | string | yes |
| **data\_provider\_org** | [data provider](global-reference.md) organization name – may be the same as [obligated party](global-reference.md) | string | yes |
| **data\_provider\_poc\_email** | email address for [data provider](global-reference.md) point of contact – may be the same as [obligated party](global-reference.md) point of contact | email | yes |
| **is\_active** | operational status of station at date entered | TRUE/FALSE | yes |
| **power\_level\_kw** | maximum charging power level of the station in kilowatts | positive float | yes |
| **num\_ports** | number of simultaneously usable ports | positive integer | yes |
| **latitude** | station latitude | latitude | yes |
| **longitude** | station longitude | longitude | yes |
| **station\_activation\_date** | The first (full or partial) day where the station is fully operable and accessible for its intended purpose | date | yes |
| **operating\_hours** | number of hours station is open per day—if not 24 (e.g., a station open from 6 AM to 6 PM is open 12 hours) | positive float | no |
| **model\_number** | charging station model number | string or integer | no |
| **serial\_number** | charging station serial number unique to charging equipment provider | string or integer | no |
| **data\_provider\_poc\_last** | last name of the [data provider](global-reference.md) point of contact | string | no |
| **data\_provider\_poc\_first** | first name of the [data provider](global-reference.md) point of contact | string | no |
| **network** | name of network service provider (if any) – may be same as [data provider](global-reference.md) | string | no |
| **network\_contact** | email address for network service provider – may be same as [data provider](global-reference.md) | email | no |
| **evse\_manufacturer** | charging equipment manufacturer name |string | no 

The port registry is a child table to station registration that includes attributes of a specific port attached to a specific station and should be collected and updated along with the station registry data. This structure accounts for stations that have multiple types of connectors.

**Table 4: Port Registration**

|**Field**  |**Definition** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**port\_id** |unique identifier for the charging port specific to *station\_id* (e.g., 1)  |ID (unique) |yes |
|**station\_id** |station identifier that corresponds to table 1 |ID (foreign) |yes |
|**connector\_type** |charging connector type  |string |yes |
|**power\_level\_kw** |maximum charging power level in kilowatts (must correspond to connector type limitations) |positive float |yes |
|**energy\_fee** |fee charged to user per kilowatt-hour |currency (USD) |no |
|**session\_fee** |fee charged to user per session |currency (USD) |no |
|**time\_fee** |fee charged to users per minute |currency (USD) |no |
|**parking\_fee** |fee charged for parking if separate from time\_fee |currency (USD) |no |
|**idle\_fee** |fee charged for minutes not charging if separate from time fee |currency (USD) |no |



# Session Data Collection

Station usage is tracked by collecting data on individual charging sessions &mdash; the period between when a user connects their vehicle (plug in) and disconnects their vehicle (plug out). The [data aggregator](global-reference.md) collects session data on a predefined schedule set by the [program administrator](global-reference.md). The data is collected and transmitted to the [data aggregator](global-reference.md) by the [data provider](global-reference.md) (or [obligated party](global-reference.md) in the case where they own and operate their stations). Session data includes key information about how, when, and, for how long a charger is in use. Session data is keyed to both the station and individual port where it occurred and inherits all above attributes of the participant, project, and site as shown in Figure 2.

**Figure 2. Session Reporting Hierarchy**
```mermaid 
graph TD

 A[...] --participant_id / project_id<br/> site_id --> B[Station] 
	 B --station_id--> D[Session i...n]
	 B --> C[Port]
		 C --port_id --> D[Session]
 ```

Session data may be transmitted to the [data aggregator](global-reference.md) by, data portal, FTP, API, email, or other data sharing procedure. While data sharing is container agnostic, session data must conform to the format described in Table 5 and should be stored in or transformable to a broadly compatible container such as a comma-separated values (CSV) file. Data delivery procedures and file formats may be further specified by the [program administrator](global-reference.md).

Refer to the [field type definitions](global-reference.md) in the global reference for more information on field types. * Additional fields may be appended as new columns as needed, but existing columns and their formats should be maintained to support interoperability.*
 
**Table 5: Session Reporting**

|**Field** |**Definition** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**session\_id** |session identifier that is unique to port\_id and station_id |ID (unique) |yes |
|**station\_id** |station identifier |ID (foreign) |yes |
|**port\_id** |port identifier that relates to station |ID (foreign) |yes |
|**plug\_start\_datetime** |date and time of session initialization (plug in)|date/time |yes |
|**charge\_start\_datetime** |date and time when charging began |date/time |yes |
|**session\_duration** |total duration of session in minutes (plug in to plug out) |non-negative float |yes  |
|**charging\_duration** |the length of time over which electricity was dispensed, measured in minutes - may not always be equal to the difference between charge\_start\_datetime  and charge\_end\_datetime due to charge interruptions or managed charging|non-negative float |yes |
|**energy\_kwh** |electricity dispensed (in kilowatt-hours) during charging session |non-negative float |yes |
|**peak\_kw** |session maximum power delivery (in kilowatts) |non-negative float |yes |
|**total\_fee\_charged** |the amount charged to the EV driver, in USD, where applicable - zero if driver was not charged for an otherwise paid charger, NULL if charger is not paid |currency (USD) |yes |
|**plug\_end\_datetime** |session end (plug out) date time |date/time |no |
|**charge\_end\_datetime** |charging end date time |date/time |no |
|**energy\_fee** |fee charged to user per kilowatt-hour |currency (USD) |no|
|**session\_fee** |fee charged to user per session |currency (USD) |no|
|**time\_fee** |fee charged to users per minute |currency (USD) |no|
|**session\_initiator** |method to initiate the charging session |string |no |
|**user\_id** |anonymized network-specific id for each unique user |string |no |
|**ended\_normally** |whether or not the session ended as expected |TRUE/FALSE |no |
|**ended\_by** |cause of the session to end (e.g., unplugged while charging). |string |no |
|**start\_soc** |battery state of charge at session start represented as a decimal between 0 and 1 |non-negative float  |no |
|**end\_soc** |battery state of charge at session end represented as a decimal between 0 and 1 |non-negative float |no |
