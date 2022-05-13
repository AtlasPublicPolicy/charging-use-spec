# Reporting Metrics

The station registration and session data can be used for several public/ratepayer-interest or programmatic reasons, such as:

- Tracking progress towards program targets and goals
- Verifying that charging stations are deployed and operating at a minimum level
- Evaluating program performance
- Informing future program design

While the specific reporting requirements will be set at the discretion of the Program Administrator (or other funding organization), this document provides a model list of reporting metrics that are supported by the Charging Use Data Specification. This list is neither meant to be prescriptive nor exhaustive but does provide a menu of potential reporting metrics that might be of interest to Program Administrators. In addition, the dependencies column provides the specific registration and session data collection fields necessary to produce those metrics.

The metrics presented here were derived from [model language](https://www.nescaum.org/documents/evse-data-collection-model-contract-provision-for-public-evse-4-16-21.pdf/) developed by the Northeast States for Coordinated Air Use Management (NESCAUM), program metrics from the Tennessee Department of Environment and Conservation, program metrics from the New York State Energy Research and Development Authority, and metrics from the [DCFC Per-Plug Incentive Program](https://jointutilitiesofny.org/ev/dcfc_incentive_program) and [EV Make-Ready Program](https://jointutilitiesofny.org/ev/make-ready) run by the Joint Utilities of New York.

Note: Program Administrators may also be interested in cost, reliability and grid impact metrics which are included in [[FORTHCOMING]](roadmap.md), [[FORTHCOMING]](roadmap.md), and [[FORTHCOMING]](roadmap.md) extensions.

## Contents
1. [Data Aggregation Levels](#data-aggregation-levels)
2. [Deployment Metrics](#deployment-metrics)
3. [Usage Metrics](#usage-metrics)
   1. [Cumulative Usage Metrics](#cumulative-usage-metrics)
   2. [Average and Median Usage Metrics](#average-and-median-usage-metrics)
   3. [Utilization Rates and Other Metrics](#utilization-rates-and-other-metrics)

## Data Aggregation Levels

Most of the metrics in this document can be aggregated at multiple levels or groupings from the individual station level to the program level, while a few such as _Average Energy Delivered per Station_ or _Stations Without Usage_are only meaningful when reported for a group of stations. Because aggregation is based on descriptive fields in the registration data such as: zip\_code, utility, site\_type, or others, it relies on accurate station registry information. Common aggregations include:

- Programmatic – These aggregations include by rebate/funding type (such as workplace, multi-unit dwelling, or highway corridor) or other programmatic divisions such as stations deployed within designated disadvantaged communities.
- Administrative – These aggregations include administrative groupings such as utility or planning region/organization.
- Other Geographic – Geographic divisions such as site, ZIP code, city, county, or census area.
- Temporal – Most data will be aggregated by reporting period. However, additional time-based aggregations include weekend/weekday or time of day.

Aggregation types are not mutually exclusive. It is often useful to cross-tabulate metrics by two or more different grouping types such as **both** by utility **and** by rebate/funding type.

## Deployment Metrics

Deployment metrics are derived from station registration data and provide high level information about program progress and performance by tracking where and what charging equipment has been deployed and program spending.

|Metric |Description &amp; purpose |Dependencies |
| --- | --- | --- |
| **Station Count** | The count of deployed stations across an aggregation group such as program, disadvantaged community, or station power level. This is a basic metric for tracking program progress towards deployment goals. | station\_id |
| **Port Count** | The count of individual simultaneously usable ports across an aggregation group such as program, disadvantaged community, or station power level. This is a basic metric for tracking program progress towards deployment goals. | num\_ports |
| **New Station Count** | The count of stations deployed within the current reporting period. | station\_id<br />station\_activation\_date |
| **New Port Count** | The count of ports deployed within the current reporting period. | num\_ports<br />station\_activation\_date |
| **Total Incentive Funding** | Cumulative sum of incentive funding spent by the program (or other grouping). This metric tracks program spending on station deployment. | primary\_funding |
| **New Incentive Funding** | Sum of incentive funding spent within the current reporting period. | primary\_funding<br />project\_funded\_date |
| **Incentive Funding Per Station/Port** | Total incentive funding divided by the total number of stations or ports deployed. This metric provides a basic cost-effectiveness measure across a group of stations. | station\_idnum\_ports<br />primary\_funding |
| **New Incentive Funding Per Station/Port** | New incentive funding divided by the number of new stations or ports deployed. This metric provides a basic cost-effectiveness measure for the reporting period across a group of stations. | station\_id<br />num\_ports<br />primary\_funding<br />project\_funded\_date |

## Usage Metrics

Usage metrics are derived from session data and provide granular information about operations and program performance as measured by how deployed stations are used.

### Cumulative Usage Metrics

Cumulative usage metrics are measures that can be summed across any level of aggregation defined in [data aggregation levels](#data-aggregation-levels) and remain interpretable. These metrics, which include fundamental productivity measures such as the count of individual sessions and the amount of energy delivered by chargers, are relevant metrics to evaluate performance from the individual station level, all the way up to the program level.

| Metric | Description &amp; purpose | Dependencies |
| --- | --- | --- |
| **Session Count** | The count of valid, discrete charging sessions within a reporting interval. This productivity metric measures how frequently a charging station (or group of stations) was used during a reporting interval. | session\_id |
| **Energy Delivered** | The sum of energy delivered by a station or group of stations within a reporting interval. This energy delivery metric can be used in program evaluation to estimate performance outcomes such as electric miles traveled and emissions reductions. Units should scale relative to level of aggregation. | energy\_kwh |
| **Time Occupied** | The sum of session duration for all sessions at a station or group of stations. This metric shows how much time within the reporting interval that a vehicle was plugged into a charger. | session\_duration |
| **Time Charging** | The sum of charging duration for all sessions at a station or group of stations. This metric shows how much time within the reporting interval that a vehicle was plugged in and charging. Units should scale relative to level of aggregation. | charging\_duration |
| **Time Idle** | Idle time is the difference between _Time Occupied_ and _Time Charging_. It measures the amount of time when a station is occupied (and therefore unavailable to other users) but not actively delivering energy. Units should scale relative to level of aggregation. | session\_durationcharging\_duration |
| **CO2e Reduction** | Equivalent mass of CO2 reduction attributable to station energy delivery. This metric is the product of _Energy Delivered_ and a program, site, or station-specific coefficient for CO2e reduction per kWh. Units should scale relative to level of aggregation. | energy\_kwh |
| **NOx Reduction** | Mass of NOx reduction attributable to station energy delivery. This metric is the product of _Energy Delivered_ and a program, site, or station-specific coefficient for NOx reduction per kWh. Units should scale relative to level of aggregation. | energy\_kwh |
| **Electric Miles Supported** | Number of electric miles supported by station energy delivery. This metric is the product of _Energy Delivered_ and a program-specific coefficient for miles per kWh. | energy\_kwh |
| **Revenue** | Sum of fees customers paid for charging sessions. This metric tracks the total amount of money, including the amount paid on a per-energy or per-time basis and any other usage fees. | total\_fee\_charged |

### Average and Median Usage Metrics

These metrics are measures of central tendency (mean and median) of usage conditioned on a second value, such as station or session. For example, energy delivered per session where energy delivery is summed over individual sessions and then divided by the count of sessions. These metrics can be calculated across different [data aggregation levels](#data-aggregation-levels), from a single station to groups of stations in the same programmatic, administrative, geographic, or temporal category. **However,  care must be taken when aggregating these metrics.** For example, the average of averages for some metrics, such as the *Average Energy Per Session*, is not a usable statistic unless the underlying individual averages are weighted. In these cases, the metric should be recomputed using the underlying data instead of aggregated from metric computed at a more granular level.

| Metric | Description &amp; purpose | Dependencies |
| --- | --- | --- |
| **Average/Median Energy Delivered per Session** | The average (or median) energy delivered (in kWh) during charging sessions at an individual or group of stations. It is a productivity metric that measures typical intensity of charging use at individual or groups of charging stations. | energy\_kwh |
| **Average/Median Energy Delivered per Station/Port** | The average (or median) energy delivered (in kWh) per station/port for a group of stations. It is a productivity metric that measures typical intensity of charging use across a group of stations (such as by geography, utility, or program). | station\_id<br />energy\_kwh |
| **Average/Median Session Duration** | The average (or median) session duration for an individual or group of chargers. It is a usage metric that measures the typical duration of sessions at an individual or group of chargers. | station\_id<br />session\_duration |
| **Average/Median Charging Duration** | The average (or median) session duration for an individual or group of stations. It is a usage metric that measures the typical duration of charging (time when energy is being delivered) at an individual or group of chargers. | station\_id<br />charging\_duration |
| **Average/Median Idle Time** | The average (or median) session duration for an individual or group of stations. It is a usage metric that measures the typical duration of charging (time when energy is being delivered) at an individual or group of chargers. | station\_id<br />session\_duration<br />charging\_duration |
| **Average/Median Unique Users by Station** | The average (or median) count of unique users by station. This metric measures typical number of unique users across a group of stations (such as by geography, utility, or program). | station\_iduser\_id |

### Utilization Rates and Other Metrics

Metrics in this section include station utilization and other metrics that could be useful in program evaluation. These metrics can be aggregated or recalculated at different [data aggregation levels](#data-aggregation-levels) , though not all metrics are meaningful or possible across all aggregation levels. For example, *Stations Without Use* can only be tracked across a group of stations as it is not meaningful for individual stations where it can only be zero or one.

| Metric | Description &amp; purpose | Dependencies |
| --- | --- | --- |
| **Occupied Utilization Rate** | The sum of _Time Occupied_ divided by the total amount of available time (defined using station open hours) within the reporting period expressed as a percentage. This metric measures the fraction of time during which a station or group of stations are occupied. | session\_duration<br />station\_id<br />operating\_hours |
| **Station Utilization Rate** | The sum of _Time Charging_ divided by the total amount of available time (defined using station open hours) within the reporting period expressed as a percentage. This metric measures the fraction of time during which a station or group of stations are occupied and actively charging. | charging\_duration<br />station\_id<br />operating\_hours |
| **Idle Utilization Rate** | The sum of _Time Idle_ divided by the total amount of available time (defined using station open hours) within the reporting period expressed as a percentage. This metric measures the fraction of time during which a station or group of stations are occupied and not actively charging. | session\_duration<br />charging\_duration<br />station\_id<br />operating\_hours |
| **Capacity Factor** | The sum of _Energy Delivered_ divided by the station&#39;s power rating multiplied by the number of available hours (defined using station open hours) expressed as a percentage. This metric provides a summary of electrical capacity utilization (ratio of energy delivered to total possible energy delivery) at an individual or group of stations. | energy\_kwh<br />station\_id<br />power\_level\_kw |
| **Site Congestion Rate** | The sum of time where all stations at a site are occupied at the same time divided by the total amount of available time (defined by station/site open hours). This metric provides a summary of time that a site is fully utilized/congested. This metric can only be calculated at the site level, though can be averaged over a group of sites. | session\_start\_time<br />session\_duration<br />site\_id |
| **Average Sessions per Day/Week** | The average (or median) number of sessions for an individual or group of stations by day or week. This metric measures usage frequency on an easy-to-interpret time basis that is different from the reporting period. | station\_id |
| **In-use Days** | The count of days within the reporting period where a station had at least one session. This metric that provides information on the regularity of charging use at a station or group of stations. | station\_id |
| **Stations Without Use** | The count of stations that had no associated sessions during the reporting period. Tracks unused station counts across a group of stations (such as by geography, utility, or program). | station\_id |
| **Unique Users** | Count of unique users that have used a station or group of stations within the reporting period. This metric measures the breadth of stations&#39; user base. Note that aggregation depends on compatible user IDs between different stations, meaning that this metric will generally not aggregate outside of a single data provider. | user\_id |

