# Electric Vehicle Charging Use Specification
A common process for collecting EV charging station use data and standardizing the metrics for reporting on EV charging station utilization.

## Introduction

Charging infrastructure deployment in the United States is expanded rapidly. Insights on the use of charging equipment are essential in order to plan for an execute the deployment of infrastructure efficiently and equitably. Many government agencies and electric utili-ties have programs to deploy charging; these programs often contain laudable goals and require data on charging use to evaluate the program’s effectiveness. A common method for collecting, validating, and sharing this charging use data can improve the efficiency and effectiveness of government and electric utility charging programs.

This specification sheet (spec sheet or spec) describes a common process for collecting EV charging station use data and standardizing the metrics for reporting on EV charging station utilization. This document contains detailed specifications for the charging equipment and use along with processes followed to transform and validate the data for reporting purposes. 

> **Box 1. Terminology & Definitions**
> Throughout the specification, the following terms are used as defined below
> - **Project or Application**: A taxonomical category, typically either a single site or small grouping of sites, as defined by a desired characteristic, such as a company or network.
> - **Site**: the physical location where one or more pieces of charging equip-ment (stations) are installed. 
> - **Station**: the single piece of charging equipment that administers charge to a vehicle; the kiosk drivers interact with to initiate charging.
> - **Port**: the piece or subdivision of the charging equipment that physically in-terfaces with a single vehicle in a one-to-one connection, usually one or two ports are present on a station.
> - **Data Collector**: entity tasked with collecting, processing, and reporting on the charging use data (i.e., the implementor of this specification).
> - **Program Operator**: entity operating of funding the charging program, typ-ically a government agency or electric utility. 

## Reporting Fields
Data can be collected from charging networks, vendors, or owner-operators (collectively referred to as participants) via web-based application programming interfaces (API), di-rect download from vendor websites, or direct data transfer from programs participants via email, file transfer protocol, or other electronic file transfer method. The tables in this spec provide definitions, expected formats or samples, and descriptions of each expected input field, as well as an overall description of the requested data.

 > **Box 2. Field Type Definitions**
 > This section refers to the following field types
 > - **String**: Text field of UTF-8 characters (letters, numbers, punctuation, and symbols). Empty string fields are <NULL>.
 > - **Numeric**: A numeric field contains only properly formatted numbers. Empty numeric fields are <NA>. Example 10 or 99 but not 099.
 > - **Float**: numeric field that may contain up to seven significant digits. Exam-ple: 1.111 or 1.1111111.
 > - **Integer**: specific numeric fields which may only contain whole numbers. Example: 2 or 5 but not 2.1.
 > - **ID**: sequence of UTF-8 characters that. ID fields labeled unique are must be unique to the conditions described in the field description. ID fields that are labeled foreign reference ID fields in other tables.
 > - **Currency**: Currency is a specialized numeric field that contains exactly two significant digits. Example: 5.00 but not 5.000 or 5
 > - **Date/time**: string field with the format: YYYYMMDD hh:mm:ss [+/-hh:mm] where time is represented by a 24 hour clock and time in brackets repre-sents the distance from coordinated universal time. Example: 20220101 01:01:01 [-5:00] represents January 1, 2022 at 12:01 AM ET.
 > - **Latitude**: WGS84 latitude in decimal degrees (EPSG:4326). Must be be-tween -90.0 and 90.0. Example: 38.889484 for the Washington Monument.
 > - **Longitude**: WGS84 longitude in decimal degrees (EPSG:4326). Must be between -180.0 and 180.0. Example -77.035278 for the Washington Mon-ument.
 > - **Email**: properly formatted email address. Example: exam-ple@example.com
 > - **TRUE/FALSE**: Boolean value symbolized by text “TRUE” or “FALSE”
 > - **ZIP Code**: valid five-digit ZIP code between 00501 and 99950. Example: 20500 for the White House.

The tables below can be incorporated into a data model that allow for aggregating across tables using relationships between tables.
  
**Figure 1: Database Schema**
