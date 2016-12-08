# LACITY Exploration 14 | Mapping LADBS Code Enforcement Cases

##Background
The Department of Building and Safety for the City of Los Angeles publishes data on cases related to Code Enforcement on building, electrical,
mechanical and zoning regulations. According to the data description, a case `may originate from a customer service request 
to investigate a possible Code violation, from a planned and authorized inspection of a neighborhood for the purpose of 
reducing blight, or from a proactive inspection of a site due to an observed hazardous condition. A case is closed 
(indicated by a "C" status) when the site satisfies the requirements for Code compliance, or when no Code violation 
is found. A case remains open (indicated by an "O" status) until the site satisfies the requirements for Code compliance.`([data.lacity.org](https://data.lacity.org/A-Safe-City/Building-and-Safety-Code-Enforcement-Case/2uz8-3tj3))

##Exploration
An exploration of the case data with data from the LA County Assessor identifying industrial properties with inquiries to:
* Identify repeat cases on an individual property
* Directly load case information from Building and Safety
* Quality issues with the data

##Methodology

### Obtaining and cleaning of data
* Data was downloaded from the City of Los Angeles's Open Data Portal
* [Original Data (Last Updated 12.5.2016 before export on 12.7.2016)](https://data.lacity.org/A-Safe-City/Building-and-Safety-Code-Enforcement-Case/2uz8-3tj3/data), can be also downloaded in this repo.
  * Approx. 12,100 rows
* Filtering necessary attributes.
 * The `Case Type` attribute contains the following ([Description Source Link](https://www.ladbs.org/docs/default-source/forms/administrative/request-to-purchase-pcis-certificate-of-occupancy-and-or-ceis-data.pdf?sfvrsn=7)):

| Case Type  | Description                              | Include |
|------------|------------------------------------------|---------|
| BILLBOARDS | Off-Site Advertisement                   | No      |
| CITATIONS  | Citations                                | Yes     |
| CNAP       | Contract Nuisance Abatement, Abandoned Building Task Force, and Problem Property Resolution Team           | Yes     |
| FRP        | [Forclosure Registry Program](http://clkrep.lacity.org/onlinedocs/2012/12-0647-S6_rpt_HCI_01-19-2016.pdf)  | No      |
| GENERAL    | General                                  | Yes     |
| PACE       | Pro-Active Code Enforcement              | Yes     |
| SIGNS      | On-Site Advertising                      | No      |
| VEIP       | Vehicle Establishment Inspection Program | No      |
| XXX        | Adult Entertainment                      | No      |

* Data was filtered and saved to this [LINK](https://data.lacity.org/A-Safe-City/ladbs_code_enforcement_filtered_1/8x82-bdqe/data), it can be downloaded in this repo.
* Data was furthered filtered by removing attributes not needed for this exploration
 * LADBS Inspection District, GIS Parcel Identification Number, Area Planning Commission
* Converting to geojson file for GIS software (QGIS, ESRI)
 * The Latitude/Longitude attribute was split into two columns, lat and long, for CSV load to GIS Software
 * A new `year` column was created based on `Date Case Generated` attribute, for visualization 
 * `ladbs_code_enforcement.geojson` generated
