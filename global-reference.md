# Glossary <a name="glossary"></a>
Throughout the specification, the following terms are used as defined below

 - **Program Administrator** - The organization that manages the charging station deployment program through which station deployments receive funding. Usually a government agency, electric utility, or an agent thereof. 
 - **Data Aggregator** - The entity tasked with collecting, processing, and reporting on the charging use data. May be the Program Administrator or a third party.
 - **Obligated Party** - The organization responsible for meeting data collection and provisioning requirements. Usually the program funding recipient.
 - **Data Provider** - The organization that collects and maintains charging use data. May be the Obligated Party or a third party vendor.
 - **Program** - Charger deployment program such as grants, rebates, or direct installation managed by the Program Administrator
 - **Project** - Collection of one or more stations at one or more sites that are attached to the same funding/rebate application or direct installation deployment. Project is defined by the Program Administrator.
 - **Site** - The common geographic place (address/parking structure/etc.) where one or more charging stations are located.
 - **Station** - The single charging unit/equipment. One charging station may have multiple charging ports.
 - **Port** - The individual plug or coupler that physically interfaces with a single vehicle in a one-to-one connection to deliver charge.
 - **Session** - A single charging event, defined as the time between plug-in and plug-out when a single vehicle is connected to a charging port. Can include charging and idle time.
 - **Charging** - When energy is flowing between the charging station and the vehicle.
 - **Idling** - When a vehicle is plugged into a charger but not receiving power. May include time before, after, or between active charging periods.
  - **Network** - Charging Network Service Provider. 
 - **Site Host** - Entity or organization that controls the property where a charging site is located. Often the same as the obligated party.
 - **Disadvantaged Community (DAC)** - Area typically identified by low-income, historic underinvestment, pollution burdened, or other indicators depending on the jurisdiction.


# Field Type Definitions <a name="types"></a>

Refer to these field type definitions for data collection formats.
 - **String** - Text field of UTF-8 characters (letters, numbers, punctuation, and symbols). Empty string fields are \<NULL>.
 - **Numeric** - A numeric field contains only properly formatted numbers. Empty numeric fields are \<NA>. 
  *Example: 10 or 99 but not 099*
 - **Float** - numeric field that may contain up to seven significant digits.  
  *Example: 1.111 or 1.1111111*
 - **Integer** - specific numeric fields which may only contain whole numbers.   
  *Example: 2 or 5 but not 2.1*
 - **ID** - sequence of UTF-8 characters. ID fields labeled unique must be unique to the conditions described in the field description. ID fields that are labeled foreign reference ID fields in other tables.
 - **Currency** - Currency is a specialized numeric field that contains exactly two significant digits.  
  *Example: 5.00 but not 5.000 or 5*
 - **Date/time** - string field with the format: YYYYMMDD hh:mm:ss [+/-hh:mm] where time is represented by a 24 hour clock and time in brackets represents the distance from coordinated universal time.  
 *Example: 20220101 01:01:01 [-5:00] represents January 1, 2022 at 12:01 AM ET*
 - **Latitude** - WGS84 latitude in decimal degrees to at least 4 decimal places ([EPSG:4326](https://epsg.io/4326)). Must be between -90.0 and 90.0.  
  *Example: 38.8894 for the Washington Monument*
 - **Longitude** - WGS84 longitude in decimal degrees to at least 4 decimal places ([EPSG:4326](https://epsg.io/4326)). Must be between -180.0 and 180.0.  
  *Example: -77.0352 for the Washington Monument*
 - **Email** - properly formatted email address.  
  *Example: example<void>@example.com*
 - **TRUE/FALSE** - Boolean value symbolized by text “TRUE” or “FALSE”
 - **ZIP Code** - valid five-digit ZIP code between 00501 and 99950.  
  *Example: 20500 for the White House*

