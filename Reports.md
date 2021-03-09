# Validation Reports

Validation reports are the products created by running processors against resources. These reports contain the details of what resource and processors were run and any issues that were found during the process.

## Overview
A list of validation reports can be accessed by clicking on the 'Validation Reports' link in the main menu on the left hand side of the Lintol interface. Each report summarises the following information in the list:

- Description (Includes Data Profile, Processor, Resource)
- Run On
- Issue indicators (Error, Warning, Information)

## Filtering
The list of reports can be refined by selecting an option from one or more of the filter dropdown inputs at the top of the list. Once an option has been selected it will automatically refine the list to reports which apply to the filtered options.

## Report Details
Validation report details can be viewed by clicking on the 'View Details' link on the right hand side of an entry in the validation report list. The header of the report contains the following information:

__Description__ - The description contains the name of the profile, the resource package name, the resource name and a number which shows the number of times the data profile has been run to create the current report.

__Ran On__ - The date and time the processor was run agains the dataset

__Source__ - The title of the source and the location of the source e.g. a CKAN instance url

The report then shows a summary of the issues that were found when running the processor. The summary splits the issues into 3 separate counts.

__Red circle__ - These are errors; issues in the dataset where data did not conform to a required expectation

__Yellow triangle__ - These are warnings; issues in the dataset where there may be data that is that does not meet expectation and requires attention or a manual review

__Green square__ - These are information points; issues were the running the processor against an item of data has produced output that provides information about the item.

## Filtering Issues
The list of issues can be refined by selecting an option from one or more of the filter dropdown inputs at the top of the list. Once an option has been selected it will automatically refine the list to issues which apply to the filtered options. The list can also be refined by entering a search term into the text input at the top of the list. As a search term is typed, the list will be refined automatically to issues in which the issue output contains the search term.

## Clean/Detailed View
When a report is displayed it will default to the "Clean" view. This summarises the report details and shows less information to keep the entry clear and concise. By clicking the 'Detailed View', a more comprehensive view of the report issues will be displayed. Clicking the 'Clean View' button will return the summariesed entries.

## Issues
The report contains a list of issues. Each issue entry contains a description of the issue and information about the entry regarding the issue. This may include metadata from the entry when returning an information issue. More details for the issue can be viewed by clicking the 'More Details' link on the right hand side of the issue entry.

The "More Details" page of a issue will give all the the summarised details plus a complete explanation of the issue and show the corresponding entry from the data where necessary.

## Links and Actions
Each report has actions which can be performed and links to other sections within the Lintol application and the source of the dataset. The actions and links are as follows:

- View Artifacts (CSV, etc.) - A modal popout will appear with links to  artifacts produced form the report
- Original Resource - A link to the original resource uploaded to CKAN
- Stored Resource - A link to the resource stored on CKAN
- Stored Package - A link to the dataset within the stored resource
- Other reports for this Resource - A link which navigates to a list of other reports that were created using the same resource as the current report
- Edit Profile - A link to the edit page for the data profile run for the current report
- Other reports for this Profile - A link which navigates to a list of other reports that were created using the same data profile as the current report