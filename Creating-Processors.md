# Coding Guidelines
These guidelines have been produced to assist in the creation of validation scripts that will be compatible with data processors in the Lintol application. Validation scripts can be written in various programming languages including Python, C, json and Ruby. The script requires a standardised output that will allow the results of the script to be consumed by the Lintol application.


## Data Processor

A data processor is an entity that contains a reference to a script that can validate an aspect of a dataset and a reference to the dataset that is to be validated.


## JSON schema

This JSON schema defines the required output from a validation script that will be readable and consumable by the Lintol application.

###Root Object

Example

```json
    {
      "version": 1,
      "item-count": 0,
      "issue-count": 0,
      "format": "",
      "info": [],
      "warnings": [],
      "errors": [],
      "supplementary":[]
    }
```

- **version** - The version number of the standardised output schema
- **item-count** - The number of items contained in the dataset
- **issue-count** - The number of information, warning or error notifications produced by the script
- **info** - A collection of information notifications produced by the script
- **warnings** - A collection of warnings produced by the script
- **errors** - A collection of errors produced by the script
- **supplementary** - A collection of additional information objects about the processor. See supplementary object


###Supplementary Object

Example

```json
    "supplementary": [
      {
        "name": "",
        "role": "",
        "source": "",
      }
    ]
```

- **name** - A name for the dataset being validated
- **role** - The type of data being validated
- **source** - A reference URL to the storage location of the dataset file

<!--
###Table Root Object

Example

```json
    "tables": [
      {
        "schema": null,
        "time": 0.03,
        "source": "data/bad_data.csv",
        "encoding": "utf-8",
        "scheme": "file",
        "errors": [],
        "format": "csv",
        "row-count": 5,
        "valid": false,
        "headers": {},
        "error-count": 1
      }
    ]
```

- **schema** -
- **time** - The amount of time required for the script to validate the table
- **source** - The local path of the dataset file
- **encoding** - The encoding format of the table
- **scheme** - The type of input used to transfer the source
- **errors** - A collection of error objects containing information about each error that was produced. See error root object
- **format** - The format of the source
- **row-count** - The number of rows contained in the table
- **valid** - A boolean value indicating if the table is valid or not
- **headers** - A key-value pair list of column headers
- **error-count** - The number of errors produced from the table
-->

### Info, Warning and Error Root Object

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


###Item Root Object

Example

```json
    "item": {
      "itemType": "",
      "location": {},
      "definition": [],
      "attributes": {}
    }
```

- **itemType** - The type of item where the error was found
- **location** - An object containing the location of the item where the error was found
- **definition** - A array containing definition information for the item that caused the error
- **attributes** - A key-value pair list of attributes to be returned


###Context Root Object

Example

```json
    "context": [
      {
        "itemType": "Row",
        "location": {},
        "definition": [],
        "attributes": {}
      }
    ]
```

- **itemType** - The type of context entity
- **location** - An object containing the location of context items
- **definition** - A array containing definition information for the context items
- **attributes** - A key-value pair list of attributes to be returned about the context items


###Minimum Sample Schema

```json
    {
      "version": 1,
      "item-count": 0,
      "issue-count": 0,
      "format": "",
      "info": [],
      "warnings": [],
      "errors": [],
      "supplementary":[]
    }
```

###Full Example Schema

```json
    {
      "version": 1,
      "item-count": 5,
      "issue-count": 1,
      "format": "csv",
      "info": [],
      "warnings": [],
      "errors": [
        {
          "processor": "csvlint",
          "code": "missing-value",
          "message": "Row 5 has a missing value in column 5",
          "item": {
            "itemType": "Cell",
            "location": {
              "column": 5,
              "row": 5
            },
            "definition": [],
            "attributes": {
              "id": "100"
            }
          },
          "context": [
            {
              "itemType": "Row",
              "location": {
                "row": 5
              },
              "definition": [],
              "attributes": {
                "id": "1"
              }
            }
          ],
          "error-data": {}
        }
      ],
      "supplementary":[
        {
          "name": "OSNI Northern Ireland Boundary",
          "role": "boundary",
          "source": "http://github.com/lintol/data/raw/bad_data.csv"
        }
      ]
    }
```
