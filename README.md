# Electric Vehicle Charging Use Specification
A common process for collecting EV charging station use data and standardizing the metrics for reporting on EV charging station utilization.

## Introduction

Charging infrastructure deployment in the United States is expanded rapidly. Insights on the use of charging equipment are essential in order to plan for an execute the deployment of infrastructure efficiently and equitably. Many government agencies and electric utili-ties have programs to deploy charging; these programs often contain laudable goals and require data on charging use to evaluate the program’s effectiveness. A common method for collecting, validating, and sharing this charging use data can improve the efficiency and effectiveness of government and electric utility charging programs.

This specification sheet (spec sheet or spec) describes a common process for collecting EV charging station use data and standardizing the metrics for reporting on EV charging station utilization. This document contains detailed specifications for the charging equipment and use along with processes followed to transform and validate the data for reporting purposes. 

> **Box 1. Terminology & Definitions**
> Throughout the specification, the following terms are used as defined below
> - **Project or Application**: A taxonomical category, typically either a single site or small grouping of sites, as defined by a desired characteristic, such as a company or network.
> - **Site**: the physical location where one or more pieces of charging equipment (stations) are installed. 
> - **Station**: the single piece of charging equipment that administers charge to a vehicle; the kiosk drivers interact with to initiate charging.
> - **Port**: the piece or subdivision of the charging equipment that physically interfaces with a single vehicle in a one-to-one connection, usually one or two ports are present on a station.
> - **Data Collector**: entity tasked with collecting, processing, and reporting on the charging use data (i.e., the implementor of this specification).
> - **Program Operator**: entity operating of funding the charging program, typically a government agency or electric utility. 

## Reporting Fields
Data can be collected from charging networks, vendors, or owner-operators (collectively referred to as participants) via web-based application programming interfaces (API), direct download from vendor websites, or direct data transfer from programs participants via email, file transfer protocol, or other electronic file transfer method. The tables in this spec provide definitions, expected formats or samples, and descriptions of each expected input field, as well as an overall description of the requested data.

 > **Box 2. Field Type Definitions**
 > This section refers to the following field types
 > - **String**: Text field of UTF-8 characters (letters, numbers, punctuation, and symbols). Empty string fields are <NULL>.
 > - **Numeric**: A numeric field contains only properly formatted numbers. Empty numeric fields are <NA>. Example 10 or 99 but not 099.
 > - **Float**: numeric field that may contain up to seven significant digits. Example: 1.111 or 1.1111111.
 > - **Integer**: specific numeric fields which may only contain whole numbers. Example: 2 or 5 but not 2.1.
 > - **ID**: sequence of UTF-8 characters that. ID fields labeled unique are must be unique to the conditions described in the field description. ID fields that are labeled foreign reference ID fields in other tables.
 > - **Currency**: Currency is a specialized numeric field that contains exactly two significant digits. Example: 5.00 but not 5.000 or 5
 > - **Date/time**: string field with the format: YYYYMMDD hh:mm:ss [+/-hh:mm] where time is represented by a 24 hour clock and time in brackets represents the distance from coordinated universal time. Example: 20220101 01:01:01 [-5:00] represents January 1, 2022 at 12:01 AM ET.
 > - **Latitude**: WGS84 latitude in decimal degrees (EPSG:4326). Must be between -90.0 and 90.0. Example: 38.889484 for the Washington Monument.
 > - **Longitude**: WGS84 longitude in decimal degrees (EPSG:4326). Must be between -180.0 and 180.0. Example -77.035278 for the Washington Monument.
 > - **Email**: properly formatted email address. Example: example@example.com
 > - **TRUE/FALSE**: Boolean value symbolized by text “TRUE” or “FALSE”
 > - **ZIP Code**: valid five-digit ZIP code between 00501 and 99950. Example: 20500 for the White House.

The tables below can be incorporated into a data model that allow for aggregating across tables using relationships between tables.
  
**Figure 1: Database Schema**
 
![Figure 1 Database Schema](https://github.com/AtlasPublicPolicy/charging-use-spec/blob/main/figure_1.png)
 
 ## Data Collection
This section describes the process by which program participants can share their charging utilization data required for reporting. This process starts with the Data Collector receiving information about participants that have entered the program. These data can be submit-ted by the Program Operator to the Data Collector in a spreadsheet form in order to initi-ate the participant into the data collection process.
 
The Data Collector then creates a _Data ID_ for each participant that will be used track the participant throughout the program and be used by the participant to submit data through the portal. The identifier will be a combination of:
1.	The first and last characters of the participants main point of contact email, be-fore the @ sign (e.g., john.doe@company.com would produce the prefix JE).
2. A sequential number with padded zeros (e.g., 000001).

Using this Data ID, the Data Collector then reaches out via email to each program partici-pant with instructions on how to submit their data. The data can be submitted through an online form, where participants are instructed to confirm their email, Data ID, and Pro-gram Operator, and to securely transfer their data so it can be queued up for validation.
 
## Participant IDs
While requirements vary, in the absence of a universal standard, a unique identifier separate from personally identifiable information (such as email, first name, or last name) is necessary to link registration and usage data. The identifier created is generated by the following method:
 > (First letter of email + last letter of email before @ + 6-digit sequential id)

Thus, for john.doe@example.com as the first participant, the generated identifier would be JE000001. The prepended letters are used to prevent accidental submission of the wrong information.

## Site, Station, and Port Registration
The key reporting unit is the charging station, which, as defined in Box 1 is the individual unit of charging equipment. For each charging station tracked, registration data will be provided by the participants to the Program Operator describing the location and type of equipment. Supplemental attributes may be included specific to the project, such as public program funding. These tables will be updated regularly by the Program Operator whenever a new station covered by the project is deployed or a new participant joins the program. The Program Operator will provide an updated inventory list to the Data Collector on a periodic basis, and new stations and participants will be added to the station database.
 
Fields to be included in the registration data tables are described in Table 1, Table 2, Table 3 and Table 4. Combined, these four tables contain all relevant attributes necessary to identify, aggregate, and analyze charging session data.
 
The first three tables are hierarchical, representing in order: 1) charging site, which is the site host location for one or more charging stations in the same network (or otherwise managed jointly), 2) individual charging station, and 3) each charging port attached to a charging station, sometimes known as a plug. Each port is uniquely linked to a charging station, which is inturn uniquely linked to a charging site. Individual entry is provided for ports to allow for flexibility on power delivery and fee structures.

Table 4 conveys program application and funding data for specific projects (charging stations funded under the same application). Projects are tied to the charging site and stations that project funded. One site might host chargers from multiple projects if additional stations are added over time. 
 
For each table the required column can be _Yes_, _No_, or _Program_ where Yes means the field must be delivered for compliance and _Program_ means the field may be required for some programs and not others. For the “Requirements and Data Format” column, any field in **bold** beginning with **Standard** is defined in Appendix A.
 
Table 1: Charging Site Registration 

|**Field** |**Description** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**site\_id** |unique identity specific to the network for the location of this charging station (may be same as application\_number in table 4) |ID (unique) |yes |
|**site\_name** |descriptive name of charging site (e.g., Mercy Hospital) |string |yes |
|**network** |entity providing charging (including “none”) |**Standard Charging Network** |yes |
|**site\_type** |type of site host for the charging site. |**Standard Site Type** |yes |
|**site\_type\_detail** |additional detail on site host land use |string |no |
|**access\_type** |Type of access available (public/unrestricted, private/restricted) |**Standard Access Type** |yes |
|**address\_1** |site address, line one |string |yes |
|**address\_2** |site address, line two |string |no |
|**city** |station city |**Standard City Type** |yes |
|**state** |station state (full name) |**Standard State Type** |yes |
|**zip\_code** |Station ZIP code |ZIP code |yes |
|**poc\_first\_name** |location site host point of contact first name |string |yes |
|**poc\_last\_name** |location site host point of contact last name |string |yes |
|**poc\_email** |location site host point of contact email address |email |yes |
|**data\_provider\_first\_name** |data provider point of contact first name |string |yes |
|**data\_provider\_last\_name** |data provider point of contact last name |string |yes |
|**data\_provider\_email** |data provider point of contact email address |email |yes |


Table 2: Charging Station Registration 

|**Field**  |**Definition** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**station\_id** |unique identifier of charging station generated upon registration (e.g., 01-000001) |ID (unique)  |yes |
|**station\_serial** |unique identifier of charging station derived from station serial number or network identifier (e.g., 123-345-2) |ID (unique) |yes |
|**station\_name** |name of charging station (e.g., Mercy Hospital – 2) |string |yes |
|**site\_id** |location identifier that corresponds to table 1 |ID (foreign) |yes |
|**org\_name** |organization name of the entity obligated to report data (more than one organization can operate a charging station at a single site) |string |yes |
|**site\_host\_name** |name of site host if different from org\_name |string |no |
|**operating\_hours** |number of hours station is open per day—if not 24 (e.g., a station open from 6 AM to 6 PM is open 12 hours)  |positive float |no |
|**latitude** |station latitude |latitude |yes |
|**longitude** |station longitude |longitude |yes |
|**station\_activation\_date** |date station was officially activated for public use |date |yes |
|**serial\_number** |charging station serial number unique to charging equipment provider |string or integer |no |
|**model\_number** |charging station model number |string or integer |no |
|**num\_ports** |number of simultaneously usable ports |positive integer |no |
|**evse\_manufacturer** |charging equipment manufacturer name |**Standard Charging Equipment Name** |no |
Table 3: Charging Port Registration 

|**Field**  |**Definition** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**port\_id** |unique identifier for the charging port specific to *station\_id* (e.g., 1)  |ID (unique) |yes |
|**site\_id** |location identifier that corresponds to table 1 |ID (foreign) |yes |
|**station\_id** |station identifier that corresponds to table 1 |ID (foreign) |yes |
|**connector\_type** |charging connector type  |**Standard Connector Type** |yes |
|**power\_level\_kw** |maximum charging power level in kilowatts (must correspond to connector type limitations) |positive float |yes |
|**energy\_fee** |fee charged to user per kilowatt-hour |currency (USD) |program |
|**session\_fee** |fee charged to user per session |currency (USD) |program |
|**time\_fee** |fee charged to users per minute |currency (USD) |program |
|**parking\_fee** |fee charged for parking if separate from time\_fee |currency (USD) |program |
|**idle\_fee** |fee charged for minutes not charging if separate from time fee |currency (USD) |program |
Table 4: Project/Application Funding and Cost 

|**Field**  |**Definition** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**project\_number** |project identifier unique to primary\_funding\_source (may be same as site\_id in table 1) |ID (unique) |yes |
|**primary\_funding\_source** |primary public funding source for the project/application |**Standard Primary Funding Source** |yes |
|**site\_id** |location identifier that corresponds to table 1 |ID (foreign) |yes |
|**covered\_stations** |single or list of station\_id (table 2) funded by project – if list, delimited by a semi-colon (E.g., 2201; 2202; 2203) |ID (foreign) |yes |
|**primary\_funding** |amount of funding station received from the primary funding source dedicated to the charging site (can include funds for installation, e.g., make-ready, equipment, and site preparation, but should not include any funding for station operation) |currency (USD) |yes |
|**utility\_makeready** |amount of funding the project received from electric utilities dedicated to infrastructure make-ready |currency (USD) |program  |
|**utility\_funding\_other** |amount of funding the project received from utility for equipment or other non-make-ready costs (should not include any funding for operational costs) |currency (USD) |program  |
|**dac\_proximate** |(For DCFC) project is located inside or within 0.5 miles of disadvantaged community as defined by local jurisdiction |TRUE/FALSE |program |
|**in\_dac** |project is located inside of disadvantaged community as defined by local jurisdiction |TRUE/FALSE |program |
|**other\_makeready** |amount of other public funding station received dedicated to infrastructure make-ready |currency (USD) |program |
|**other\_funding\_other** |amount of other public funding project received for equipment or other non-make-ready costs (should not include any funding for operational costs) |currency (USD) |program  |
|**cost\_share** |funding amount project has received from other (private, non-utility) sources when combined with primary\_funding and utility\_funding and other\_public\_funding equals the total cost of the charging installation |currency (USD) |program |


Table 5: Charging Station De-Registration 

|**Field**  |**Definition** |**Data Format** |**Required** |
| :- | :- | :- | :- |
|**station\_id** |identifier of charging station in table 2 (e.g., 123-345-2) |ID (foreign) |yes |
|**station\_name** |name of charging station (e.g., Mercy Hospital – 2) |string |yes |
|**site\_id** |location identifier of charging station in table 1 |ID (foreign) |yes |
|**station\_deactivation\_date** |date station was officially activated for public use |date |yes |
|**serial\_number** |charging station serial number unique to charging equipment provider |string or integer |no |
|**station\_status** |what was done with the station |REMOVED, REPLACED, MOVED |yes |
