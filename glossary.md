# Glossary
Throughout the specification, the following terms are used as defined below
 - **Charging** - When energy is flowing between the charging station and the vehicle.
 - **Connector** - The physical plug/coupler configuration - either standards-based or proprietary.
 - **Data Provider** - The organization that collects and maintains charging use data. May be the Obligated Party or a third party vendor.
 - **Disadvantaged Community (DAC)** - Area typically identified by low-income, historic underinvestment, pollution burdened, or other indicators depending on the jurisdiction.
 - **Idling** - When a vehicle is plugged into a charger but not receiving power. May include time before, after, or between active charging periods.
 - **Network** - Charging Network Service Provider. 
 - **Port** - The component or system on a charger capable of connecting to and charging charging a single EV on a one-to-one basis. Ports are the basic data-generating unit of charging equipment. One port may connect to vehicles using more than one connector type, but only one connector type may be used at a time.
 - **Program** - Charger deployment program such as grants, rebates, or direct installation managed by the Program Administrator
 - **Project** - Collection of one or more stations at one or more sites that are attached to the same funding/rebate application or direct installation deployment. Project is defined by the Program Administrator.
 - **Reporting Period** - the program-defined time interval over which data is reported. The reporting period defines the frequency of data collection (e.g. monthly, quarterly, biannually)
 - **Session** - A single charging event, defined as the time between plug-in and plug-out when a single vehicle is connected to a charging port. Can include charging and idle time.
 - **Site Host** - Entity or organization that controls the property where a charging station is located. Often the same as the obligated party.
 - **Station** - The single physical place (address/parking structure/etc.) where charging equipment containing one or more ports is located.


## Specification Roles
The specification outlines four (4) specific roles in the data collection and reporting process. The roles fall into two (2) categories.
*  **Implementers** — which includes the **Program Administrator** and the **Data Aggregator**
*  **Participants** — which includes the **Obligated Party** and the **Data Provider**

Each role may be filled by a different organization, or one organization may cover the responsibilities of both roles within a category. Table 1 provides a description of each role and their general responsibilities. In both categories, there may be opportunities for responsibilities to be delegated between roles within the same category.

**Table 1: Roles and Responsibilities**

| **Role** | **Description** | **Responsibilities**
| --- | --- | --- | 
| **Program Administrator** | The organization that manages the charging station deployment program through which station deployments receive funding. Usually a government agency, electric utility, or an agent thereof. | Onboard participants.</br></br> Collect inventory data and submit to data aggregator (in compliant format).</br></br> Set rules and requirements for data reporting. </br></br> Ensure compliance.
| **Data Aggregator** | The entity tasked with gathering, processing, and reporting on the charging use data. Often a third-party contractor, though might also be the same as the Program Administrator.  | Gather inventory data from Program Administrator.</br></br> Gather operational data from participants.</br></br> Validate, clean, and transform data.</br></br>Generate reports and submit Program Administrator.
| **Obligated Party** | The organization responsible for meeting data collection and provisioning requirements. Usually the program funding recipient. | Gather and submit inventory information to Program Administrator.</br></br> Collect operations cost data and submit to Data Aggregator (in compliant format).</br></br> Ensure Data Provider is meeting reporting requirements.
| **Data Provider** |   The organization that collects and maintains charging use data. Often will be a third party vendor such as a network service provider but may be the Obligated Party if stations are not networked. | Gather and submit inventory information to Program Administrator.</br></br> Collect session data and report to Data Aggregator (in compliant format).


