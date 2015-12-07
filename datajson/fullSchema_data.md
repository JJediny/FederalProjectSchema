---
"$schema": http://json-schema.org/draft-04/schema#
id: http://project-open-data.github.io/schema/1_0_final/single_entry.json#
title: Common Core Metadata Schema
description: The metadata format for all federal open data. Validates a single JSON
  object entry (as opposed to entire Data.json catalog).
type: object
required:
- title
- description
- keyword
- modified
- publisher
- contactPoint
- mbox
- identifier
- accessLevel
properties:
  accessLevel:
    description: 'The degree to which this dataset could be made publicly-available,
      regardless of whether it has been made available. Choices: public (Data asset
      is or could be made publicly available to all without restrictions), restricted
      public (Data asset is available under certain use restrictions), or non-public
      (Data asset is not available to members of the public)'
    title: Public Access Level
    enum:
    - public
    - restricted public
    - non-public
  accessLevelComment:
    title: Access Level Comment
    description: An explanation for the selected "accessLevel" including instructions
      for how to access a restricted file, if applicable, or explanation for why a
      "non-public" or "restricted public" data assetis not "public," if applicable.
      Text, 255 characters.
    anyOf:
    - type: string
      minLength: 1
      maxLength: 255
    - type: 'null'
  accessURL:
    title: Download URL
    description: URL providing direct access to the downloadable distribution of a
      dataset.
    anyOf:
    - type: string
      format: uri
    - type: 'null'
  accrualPeriodicity:
    title: Frequency
    description: Frequency with which dataset is published.
    anyOf:
    - enum:
      - Annual
      - Bimonthly
      - Semiweekly
      - Daily
      - Biweekly
      - Semiannual
      - Biennial
      - Triennial
      - Three times a week
      - Three times a month
      - Continuously updated
      - Monthly
      - Quarterly
      - Semimonthly
      - Three times a year
      - Weekly
      - Completely irregular
    - type: 'null'
  bureauCode:
    title: Bureau Code
    description: Federal agencies, combined agency and bureau code from <a href="http://www.whitehouse.gov/sites/default/files/omb/assets/a11_current_year/app_c.pdf">OMB
      Circular A-11, Appendix C</a> in the format of <code>015:010</code>.
    anyOf:
    - type: array
      items:
        type: string
        pattern: "[0-9]{3}:[0-9]{2}"
      minItems: 1
      uniqueItems: true
    - type: 'null'
  contactPoint:
    title: Contact Name
    description: Contact person’s name for the asset.
    type: string
  dataDictionary:
    title: Data Dictionary
    description: URL to the data dictionary for the dataset or API. Note that documentation
      other than a data dictionary can be referenced using Related Documents as shown
      in the expanded fields.
    anyOf:
    - type: string
      format: uri
    - type: 'null'
  dataQuality:
    title: Data Quality
    description: Whether the dataset meets the agency’s Information Quality Guidelines
      (true/false).
    anyOf:
    - type: boolean
    - type: 'null'
  description:
    title: Description
    description: Human-readable description (e.g., an abstract) with sufficient detail
      to enable a user to quickly understand whether the asset is of interest.
    type: string
  distribution:
    title: Distribution
    description: Holds multiple download URLs for datasets composed of multiple files
      and/or file types
    anyOf:
    - type: array
      items:
        type: object
        required:
        - accessURL
        - format
        properties:
          accessURL:
            title: Download URL
            description: URL providing direct access to the downloadable distribution
              of a dataset.
            type: string
            format: uri
          format:
            title: Format
            description: The file format or API type of the distribution.
            pattern: "^[-\\w]+/[-\\w]+(\\.[-\\w]+)*([+][-\\w]+)?$"
            type: string
      minItems: 1
      uniqueItems: true
    - type: 'null'
  format:
    title: Format
    description: The file format or API type of the distribution.
    anyOf:
    - pattern: "^[-\\w]+/[-\\w]+(\\.[-\\w]+)*([+][-\\w]+)?$"
      type: string
    - type: 'null'
  identifier:
    title: Unique Identifier
    description: A unique identifier for the dataset or API as maintained within an
      Agency catalog or database.
    type: string
    pattern: "[\\w]+"
  issued:
    title: Release Date
    description: Date of formal issuance.
    anyOf:
    - type: string
  keyword:
    title: Tags
    description: Tags (or keywords) help users discover your dataset; please include
      terms that would be used by technical and non-technical users.
    type: array
    items:
      type: string
      minLength: 1
    minItems: 1
  landingPage:
    title: Homepage URL
    description: Alternative landing page used to redirect user to a contextual, Agency-hosted
      “homepage” for the Dataset or API when selecting this resource from the Data.gov
      user interface.
    anyOf:
    - type: string
      format: uri
    - type: 'null'
  language:
    title: Language
    description: The language of the dataset.
    anyOf:
    - type: array
      items:
        type: string
    - type: 'null'
  license:
    title: License
    description: The license dataset or API is published with. See <a href="http://project-open-data.github.io/open-licenses/">Open
      Licenses</a> for more information.
    anyOf:
    - type: string
      minLength: 1
    - type: 'null'
  mbox:
    title: Contact Email
    description: Contact person’s email address.
    type: string
    format: email
  modified:
    title: Last Update
    description: Most recent date on which the dataset was changed, updated or modified.
    anyOf:
    - type: string
  PrimaryITInvestmentUII:
    title: Primary IT Investment UII
    description: For linking a dataset with an IT Unique Investment Identifier (UII)
    anyOf:
    - type: string
      pattern: "[0-9]{3}-[0-9]{9}"
    - type: 'null'
  programCode:
    title: Program Code
    description: Federal agencies, list the primary program related to this data asset,
      from the <a href="http://goals.performance.gov/sites/default/files/images/FederalProgramInventory_FY13_MachineReadable_091613.xls">Federal
      Program Inventory</a>. Use the format of <code>015:001</code>
    anyOf:
    - type: array
      items:
        type: string
        pattern: "[0-9]{3}:[0-9]{3}"
      minItems: 1
      uniqueItems: true
    - type: 'null'
  publisher:
    title: Publisher
    description: The publishing entity.
    type: string
  references:
    title: Related Documents
    description: Related documents such as technical information about a dataset,
      developer documentation, etc.
    anyOf:
    - type: array
      items:
        type: string
        format: uri
      minItems: 1
      uniqueItems: true
    - type: 'null'
  spatial:
    title: Spatial
    description: The range of spatial applicability of a dataset. Could include a
      spatial region like a bounding box or a named place.
    anyOf:
    - type: string
      minLength: 1
    - type: 'null'
  systemOfRecords:
    title: System of Records
    description: If the systems is designated as a system of records under the Privacy
      Act of 1974, provide the URL to the System of Records Notice related to this
      dataset.
    anyOf:
    - type: string
      minLength: 1
    - type: 'null'
  temporal:
    title: Temporal
    description: The range of temporal applicability of a dataset (i.e., a start and
      end date of applicability for the data).
    anyOf:
    - type: string
  theme:
    title: Category
    description: Main thematic category of the dataset.
    anyOf:
    - type: array
      items:
        type: string
        minLength: 1
      minItems: 1
      uniqueItems: true
    - type: 'null'
  title:
    title: Title
    description: Human-readable name of the asset. Should be in plain English and
      include sufficient detail to facilitate search and discovery.
    type: string
  webService:
    title: Endpoint
    description: Endpoint of web service to access dataset.
    anyOf:
    - type: string
      format: uri
    - type: 'null'
