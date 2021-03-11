# Coding Guidelines
These guidelines have been produced to assist in the creation of validation scripts that will be compatible with data processors in the Lintol application. Validation scripts can be written in various programming languages including Python, C, json and Ruby. The script requires a standardised output that will allow the results of the script to be consumed by the Lintol application.


## Data Processor

A data processor is an entity that contains a reference to a script that can validate an aspect of a dataset and a reference to the dataset that is to be validated.


## JSON schema

This JSON schema defines the required output from a validation script that will be readable and consumable by the Lintol application.

### Root Object

Example

```json
    {
      "version": 1,
      "item-count": 0,
      "counts": {},
      "valid": false,
      "issues-skipped": {},
      "artifacts": {},
      "tables": [],
      "filename": "",
      "preset": "",
      "table-count": 1,
      "time": 0,
      "supplementary":[]
    }
```

- **version** - The version number of the standardised output schema
- **item-count** - The number of items contained in the dataset
- **counts** - The number of information, warning or error notifications produced by the script
- **valid** - An overall assessment of the dataset
- **issues-skipped** - A count of issues either included or not included in the report with a total count
- **artifacts** - A collection of outputs from the report, normally a file e.g. a csv
- **tables** - A collection of outputs from each processor in the data profile
- **filename** - The name of the file containing the data source
- **preset** - A selection of a preset value for the type of data being processed e.g tabular
- **table-count** - The number of tables returned in the report
- **time** - The time it took to run the report in seconds
- **supplementary** - A collection of additional information objects about the processor.


### Tables Object

Example

```json
    "tables": [
      {
        "format": "csv",
        "errors": [],
        "warnings": [],
        "informations": [],
        "headers": [],
        "source": "",
        "time": 0,
        "valid": false,
        "scheme": "",
        "encoding": "",
        "schema": null,
        "item-count": 0,
        "error-count": 0,
        "warning-count": 0,
        "information-count": 0
      }
    ]
```

- **format** - The format of the data being processed e.g. csv
- **errors** - A collection of error objects containing information about each error that was produced
- **warnings** - A collection of warning objects containing information about each warning that was produced
- **informations** - A collection of information item objects containing information about each information item that was produced
- **headers** - A key-value pair list of column headers
- **source** - The local path of the dataset file
- **time** - The amount of time required for the script to validate the table
- **valid** - A boolean value indicating if the table is valid or not
- **scheme** - The type of input used to transfer the source
- **encoding** - The encoding format of the table
- **schema** - The schema of the data being processed e.g. file
- **item-count** - The number of rows contained in the table
- **error-count** - The number of errors produced from the table
- **warning-count** - The number of warnings produced from the table
- **information-count** - The number of information items produced from the table


### Information, Warning and Error Object

Example

```json
    "info": [
      {
        "processor": "",
        "code": "",
        "message": "",
        "item": {},
        "context": [],
        "error-data": {}
      }
    ]
```

- **processor** - The processor that returned the error
- **code** - A code assigned to the error
- **message** - A human readable message created to explain the error in natural language
- **item** - An object containing additional details about the error, see item root object
- **context** - A collection of objects containing context information of the error, see context root object
- **error-data** - A machine-readable version of the error “message”  
  

### Item Object

Example

```json
    "item": {
      "entity": {
        "type": "Cell",
        "location": {
            "row": 1,
            "column": 1
        },
        "definition": ""
      },
      "properties": {
        "_content": ""
      }
    }
```

- **type** - The type of item where the error was found
- **location** - An object containing the location of the item where the error was found
- **definition** - A definition for the item that caused the error
- **attributes** - A key-value pair list of attributes to be returned


### Context Object

Example

```json
    "context": [
      "item": {
        "entity": {
          "type": "Row",
          "location": {
              "row": 1,
              "column": null
          },
          "definition": ""
        },
        "properties": {
          "_content": ""
        }
      }
    ]
```

- **type** - The type of context entity
- **location** - An object containing the location of context items
- **definition** - A definition for the context items
- **attributes** - A key-value pair list of attributes to be returned about the context items


### Supplementary Object

Example

```json
    "supplementary": [
      {
        "type": "",
        "source": "",
        "name": ""
      }
    ]
```

- **type** - The type of data being validated
- **source** - A reference URL to the storage location of the dataset file
- **name** - A name for the dataset being validated


### Minimum Sample Schema

```json
    {
      "version": 1,
      "item-count": 0,
      "counts": {
        "errors": 0,
        "warnings": 0,
        "informations": 0,
      },
      "valid": false,
      "issues-skipped": {},
      "artifacts": {},
      "tables": [],
      "filename": "source_data.csv",
      "preset": "tabular",
      "table-count": 1,
      "time": 10,
      "supplementary":[]
    }
```

### Full Example Schema

```json
    {
      "supplementary": [],
      "item-count": 200,
      "error-count": 200,
      "counts": {
        "errors": 100,
        "warnings": 100,
        "informations": 0
      },
      "valid": false,
      "issues-skipped": {
        "dfi/resource-defects:1|missing-official-section-code": [
          1904,
          100,
          2004
        ]
      },
      "artifacts": {
        "dfi/resource-defects:1#report:csv": {
          "uri": "doorstep/doorstep-508b60b7-0e04-465e-843c-70daff6e064c/b6f231ce-0ca6-462c-97ae-dddd04b342b5/artifact_0",
          "is_bytes": false,
          "mime": "text/csv",
          "encoding": "utf-8"
        }
      },
      "tables": [
        {
          "format": "csv",
          "errors": [
            {
              "processor": "dfi/resource-defects:1",
              "code": "missing-official-section-code",
              "message": "The section code (prefix for SECTION_NAME) in this row is not found in the official list",
              "item": {
                "entity": {},
                "properties": null
              },
              "context": [
                {
                  "entity": {},
                  "properties": null
                }
              ],
              "error-data": {
                "export-columns": [
                  [
                    "SECTION_CODE",
                    "7125A0509_04"
                  ]
                ]
              }
            },
          ],
          "warnings": [],
          "informations": [],
          "row-count": null,
          "headers": [
            "INSTRUCTION_REFERENCE",
            "DEFECT_DETAIL",
            "SECTION_NAME",
            "DIVISION",
            "SECTION_OFFICE",
            "RECORDED_DATE",
            "DEFECT_STATUS",
            "EASTING",
            "NORTHING",
            "SECTION_CODE",
            "OFF_SECTION_NAME"
          ],
          "source": "Surface_Defects_2016.csv",
          "time": 0,
          "valid": false,
          "scheme": "file",
          "encoding": "utf-8",
          "schema": null,
          "item-count": 200,
          "error-count": 100,
          "warning-count": 100,
          "information-count": 100
        }
      ],
      "filename": "Surface_Defects_2016.csv",
      "preset": "tabular",
      "warnings": [],
      "table-count": 1,
      "time": 0
    }
```
