# Field Type Definitions
Refer to these field type definitions for data collection formats.
- **boolean** – A binary true/false value (TRUE or FALSE).
- **datetime** – A timestamp in ISO 8601/RFC 3339 format (YYYY-MM-DDThh–mm–ss.sssZ) and in coordinated universal time (UTC). For dates without time information, HH–mm–ss may be omitted. Example 2022-01-01T01–01–00Z represents January 1, 2022 at 12–01 UTC.
- **float/(n)** – A floating point number. Float fields with a number in parenthesis (n) must contain exactly n decimal places. Example 1.2345.
- **integer** – An integer number (may not contain decimal digits). Example 12345.
- **string/(n)** – A string of UTF-8 characters. String fields with a number in parenthesis (n) must contain exactly n characters.

# Valid Entry Reference
Refer to these valid entry references to ensure data is reported in expected formats and types.

- **ZIP Code** – Standard 5-digit U.S. Postal Code.
- **State Code** – Standard 2-character code for U.S. states and territories.
- **Connector Type** – One of the following values:
    - CCS
    - CHAdeMO
    - J1772
    - NACS
- **Charger Type** – One of the following values:
    - level_1
    - level_2
    - DCFC
- **Access Type** – One of the following values:
    - public
    - private
    - semi_public
    - commercial_only
- **Operating Status** – One of the following values:
    - operational
    - under_construction
    - planned
    - decommissioned
 - **Distribution Energy Resource Type** – One of the following values:
    - solar
    - stationary_battery
    - wind
    - fuel_cell
    - other 
- **Payment Method** – One of the following values:
    - cash
    - credit_card_terminal
    - membership
    - application
    - phone
    - plug-charge
    - roaming
    - other

