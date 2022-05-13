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
