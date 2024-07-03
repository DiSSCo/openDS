
This section includes the data model for different FAIR Digital Objects. 

## Directory Structure

- **developer-schema/**: Includes schemas intended for developers working with the data model.
- **fdo-profile/**: This directory contains FDO profiles, defining the metadata and structural requirements for various FDO types.
- **fdo-type/**: Contains specific schemas for different types of FDOs, including digital specimens.
  - **digital-specimen/**: Contains schemas related to digital specimens, such as:
    - `chronometric-age.json`
    - `digital-specimen.json`
    - `event.json`
    - `identification.json`
    - `location.json`
    - `material-entity.json`
- **internal-schema/**: Internal schemas used for system processes and internal data handling.
- **nginx/**: Configuration files for the Nginx server used in the deployment of the data model services.
- **Dockerfile**: A Dockerfile for building and deploying the data model services in a containerized environment.


## Data Modeling Approach

Our approach to data modeling involves:

1. **Reviewing Existing Standards**: We review existing terms and standards such as Darwin Core and ABCD to identify relevant concepts and definitions.
2. **Harmonisation**: We harmonise these existing terms to create a specification that meets the needs of digital specimens lifecycle in the DiSSCo infrastructure.
3. **Specification Development**: Based on the harmonised terms, we develop detailed specifications and schemas that define the structure and content of digital specimens and related data. Our schemas are versioned (each object schema is individually versioned) and maintained in this repository, and published in the [schema repository](https://schemas.dissco.tech/).

