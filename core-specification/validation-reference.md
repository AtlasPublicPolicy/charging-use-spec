# Data Validation

This section describes the individual validations to be performed on the registration and session data that ensure that they conform to specifications and that measurements fall within expected parameters. Data received by the data aggregator may have quality issues caused by measurement or data processing errors that interfere with successful data ingestion or the calculation of valid reporting metrics.

The data validation process performs a series of automated checks on the received data, flagging it as erroneous or non-compliant if such checks fail. Data that passes all validation checks will be considered validated data, meaning that the data aggregator has identified it as compliant with the charging use data specification and certified its use in reporting.

Validations for data fields return one of three results:

![](https://via.placeholder.com/15/09692e/000000?text=+)  **Valid** – entry conforms to expected type, format, and parameters   
![](https://via.placeholder.com/15/ffc800/000000?text=+)  **Warning** – entry exceeds parameter(s) range and requires manual quality assurance check  
![](https://via.placeholder.com/15/c40404/000000?text=+)  **Error** – required data missing or not conformant to expected type, format, or parameters  

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
| **Chronologically Inconsistent Start and End Datetimes** | plug\_start\_datetime<br />plug\_end\_datetime<br />charge\_start\_datetime<br />charge\_end\_datetime | consistency | The plug_end_datetime or charge_end_datetime  value occurs prior to the respective plug_start_datetime or charge_start_datetime value. |
| **No Matching Registration** | station\_id | cross reference | The session station\_id is not in the program station registry. |
| **Zero Length Session Duration** | session\_duration<br />charging\_duration | constraint | The session\_duration or charging\_duration values are zero. |
| **Zero Energy Session** | energy\_kwh | constraint | The energy\_kwh value is zero. |
