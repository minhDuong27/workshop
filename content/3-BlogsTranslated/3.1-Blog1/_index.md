
---
title: "Blog 1 - Carbon Methodology Update for AWS Customer Carbon Footprint Tool"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Carbon Methodology Update for the AWS Customer Carbon Footprint Tool

**By Margaret O’Toole, Alexis Bateman, Marta Fraga, and Paula Csatlos – April 23, 2025 – Featured, Sustainability**

To support our customers’ sustainability journeys, we launched the **Customer Carbon Footprint Tool (CCFT)** in the AWS Billing and Cost Management Console in 2022.  
CCFT is a tool that helps customers track, measure, and review the carbon emissions generated from their use of AWS.  
The CCFT accounts for **Scope 1** and **Scope 2** emissions as defined by the Greenhouse Gas Protocol, covering the full range of AWS products, including Amazon EC2, Amazon S3, AWS Lambda, and others.  
Emissions are expressed in **metric tons of carbon dioxide equivalent (MTCO2e).**

Today, we are announcing three updates as part of our ongoing effort to improve CCFT:

- **Easier data access:** Customers can now access their emissions data more easily through Billing and Cost Management Data Exports.  
- **More granular carbon data:** We’ve increased the level of detail in CCFT to show emissions by AWS Region.  
- **Updated, independently verified methodology:** We are releasing an updated allocation methodology (v2.0), along with a methodology document and assurance, verified by APEX.

As a result of these changes, customers will see carbon emissions calculated using the new methodology for their AWS usage beginning January 2025, and some may notice a change in their estimated emissions.  
Following industry best practices, CCFT data for December 2024 and earlier will continue to use methodology version 1.0.

---

## Details of Today’s CCFT Update

### 1. Easier Data Access
To simplify how customers use data from CCFT, they can now export data starting from January via the AWS **Data Exports** service in Billing and Cost Management.  
The exported carbon emissions data provides estimated emissions for all member accounts linked to the management account when customers use **AWS Organizations**.

The **Data Exports** service automatically delivers monthly updates in **CSV or Parquet** format to **Amazon S3**, allowing customers to automate carbon data processing across their entire AWS organization.  
With the first export, they’ll receive up to **38 months of historical data** in the S3 bucket for historical analysis.  
Data for December 2024 and earlier is calculated using methodology v1.0, while data from January 2025 onward uses v2.0.

Customers can learn more about setting up Data Exports in the [Data Exports User Guide](#).

---

### 2. Regional Granularity
Customers can now view carbon emissions broken down by **AWS Region** (for example, *US East (Ohio)*), with **Amazon CloudFront CDN** usage shown as a separate **Global Services** category.  
This helps customers identify which regions contribute most to their carbon footprint and reconsider workload distribution across AWS Regions.

---

### 3. Updated Methodology v2.0
Customers often use a wide range of AWS services across multiple regions, making it challenging to track and allocate carbon emissions based on workloads.

While there is no single industry standard for allocating cloud-related emissions to customers, the updated **v2.0 methodology** leverages existing standards to support CCFT, including:  
**GHG Protocol Corporate Standard, GHG Protocol Product Standard, ISO 14040/44 (LCA), ISO 14067 (Product Carbon Footprint),** and **ICT Sector Guidance.**

Customers can read more in the *full-length methodology document*, but here’s a brief overview of the approach:

---

#### Scope 1 Overview (Direct Emissions)
Scope 1 includes direct emissions from sources owned or controlled by AWS, such as fuel combustion in backup generators at data centers.  
AWS receives Scope 1 activity data for the previous year during the first quarter of the following year — as part of Amazon’s annual company-wide verification process.  
We then calculate estimated carbon data at the **site level**, aggregating results up to the **cluster level**.

An AWS cluster can represent a region (e.g., *us-east-1, eu-central-1*) or a CloudFront Edge cluster (e.g., *CF North America, CF South America*).

---

#### Scope 2 Overview (Indirect Emissions)
Scope 2 covers indirect emissions from purchased electricity, and CCFT applies the **market-based approach**.  
For example, grid mixes (the percentage of carbon-free energy in the local grid) and **emission factors (kgCO2e/kWh)** are updated annually and verified as part of Amazon’s carbon footprint assurance process.  
For Scope 2, CCFT uses location-based emission factors and follows the priority order recommended by the Greenhouse Gas Protocol.

---

#### Allocation Model Overview (v2.0)
The model first allocates estimated emissions at the **cluster level** to **server racks** within that cluster, then maps those emissions to specific AWS services based on resource utilization of the racks.  
It also considers dependencies between foundational services with dedicated hardware (e.g., Amazon EC2) and higher-level services built on top of them (e.g., AWS Lambda).  
Finally, emissions are attributed to individual **customer accounts** consuming those services.

**The model works as follows:**
1. Allocate estimated cluster-level emissions to server racks within the cluster.  
2. Allocate carbon emissions from racks to AWS cloud services based on resource usage, accounting for service interdependencies.  
3. Allocate estimated carbon emissions for each service to the respective customer accounts consuming those services.

Some customers may notice changes in their estimated emissions as the new CCFT methodology (v2.0) enables more accurate attribution of emissions, better reflecting their actual AWS service usage.

---

### Key Updates in Methodology v2.0

1. **Unused Capacity Allocation:**  
   We now allocate unused capacity emissions across all AWS customers.  
   AWS prepares sufficient server rack capacity to meet customer demand — sometimes resulting in unused capacity.  
   The estimated carbon emissions associated with this unused capacity are now proportionally allocated to all customers using AWS services.

   This aligns with the GHG Protocol, ISO standards on product-level carbon reporting (ISO 14040 / 14044), and cloud/data center sector guidance, which require inclusion of inefficiencies necessary to deliver products and services to customers.

2. **Improved Allocation Logic:**  
   Enhanced logic for distributing estimated emissions from AWS services without dedicated hardware (like AWS Lambda or Amazon Redshift) between AWS customers and internal Amazon teams.

3. **Shared Overhead Allocation:**  
   Updated allocation for shared overhead emissions related to data center operations, such as emissions from networking racks and regional expansion activities supporting AWS customers.

---

We will continue improving our tools based on customer needs.  
Customers can learn more about these updates by reading the *methodology document* and consulting both the *CCFT User Guide* and *Data Exports User Guide*.

Looking ahead, we will keep publishing methodology updates based on evolving data, climate science, and continue investing in features and capabilities that support customers on their sustainability journey.

---

### Commitment to The Climate Pledge
To learn more about **The Climate Pledge** — Amazon’s commitment to becoming **net-zero carbon by 2040** — and our broader sustainability investments across all business areas, including AWS, please visit our [sustainability site](#).
