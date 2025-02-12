# StellarBlue Timeseries App

### :ledger: Description 
This Vue.js application is intended to visualize time-series data. It features a table for showing time-series values and a line chart for trend analysis.

## Core Requirements
- **Framework Choice**: This application is built using Vue.js.
- **Data Representation**:
  - The application utilizes a JSON file comprising 3 timeseries datasets, each with timestamps and values.   
  - Timeseries values are displayed in a table.
  - The data is visualized in a line chart to depict trends over time.
 
## Enhanced Features
- **Interactive Data Control**:
  - Made the table editable, allowing users to update any value in the timeseries. The chart automatically updates to reflect changes.
  - Added validation for table input values, restricting inputs to arithmetic values within the range [-2000, 2000]. If the input is invalid, the app displays a validation message and prevents updates to the table and chart.
  - Included legend checkboxes for each timeseries, enabling users to show or hide specific timeseries only in the chart for better data control.

###  :wrench: Development


### :question: FAQ
If there are any questions, create an issue in this repository.

