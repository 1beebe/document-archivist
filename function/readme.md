# Convert Array to CSV - Function Documentation

## Overview

This function converts a JavaScript array of objects into a properly formatted CSV (Comma-Separated Values) string. The function uses the keys from the first object in the array as column headers and processes all subsequent objects according to this column structure.

## How It Works

1. **Column Detection**: The function examines the first object in your array and uses its keys as the CSV column headers
2. **Data Processing**: Each object in the array is converted to a CSV row, with values mapped to the appropriate columns
3. **CSV Formatting**: All values are properly escaped according to CSV standards (handling commas, quotes, and newlines)
4. **Output**: The resulting CSV string is stored in a variable you specify

## Configuration Options

### Input Array
**Type:** Variable Selection (Array)  
**Required:** Yes

Select the array of objects you want to convert to CSV. This must be:
- An array with at least one element
- Each element must be an object (not a primitive value or nested array)
- The first object's keys will define the column structure for the entire CSV

**Example:**
```javascript
[
  { name: "John", email: "john@example.com", age: 30 },
  { name: "Jane", email: "jane@example.com", age: 25 }
]
```

### Output Variable Name
**Type:** Text Input  
**Required:** Yes

Specify the name of the variable that will store the generated CSV text. You can use this variable in subsequent workflow steps to save to a file, send via email, or process further.

**Example:** `csvOutput`, `exportedData`, `customerCSV`

## Output

The function creates a single output variable (with the name you specified) containing the complete CSV string.

**Output Format:**
- First line: Column headers (comma-separated)
- Subsequent lines: Data rows (comma-separated)
- Lines separated by newline characters (`\n`)

**Example Output:**
```
name,email,age
John,john@example.com,30
Jane,jane@example.com,25
```

## CSV Formatting Rules

The function automatically handles special characters according to CSV standards:

- **Commas**: Values containing commas are wrapped in double quotes
- **Quotes**: Double quotes within values are escaped by doubling them (`""`)
- **Newlines**: Values containing newlines are wrapped in double quotes
- **Null/Undefined**: Converted to empty strings
- **Numbers/Booleans**: Converted to their string representations

**Example:**
```javascript
Input:  { field: 'Value with, comma and "quote"' }
Output: "Value with, comma and ""quote"""
```

## Important Behaviors

### Column Structure
The columns are determined **exclusively** by the first object in the array. If subsequent objects:
- Have additional keys not in the first object: Those keys are ignored
- Are missing keys from the first object: Those cells will be empty in the CSV

**Example:**
```javascript
[
  { name: "John", email: "john@example.com" },  // Defines columns: name, email
  { name: "Jane", phone: "555-1234" }           // phone is ignored, email is empty
]

Result:
name,email
John,john@example.com
Jane,
```

### Data Type Handling
All values are converted to strings:
- `null` → empty string
- `undefined` → empty string
- `true` → "true"
- `123` → "123"
- Objects/Arrays → their string representation

## Error Conditions

The function will throw an error if:
- No input array is provided
- The input is not an array
- The array is empty
- The first element is not an object

## Console Output

The function logs progress information:
- When conversion starts
- Number of objects being processed
- Column headers detected
- Completion message with total row count

## Use Cases

- **Data Export**: Export database query results or API responses to CSV
- **Report Generation**: Create CSV reports from processed data
- **Data Integration**: Prepare data for import into spreadsheet applications
- **Batch Processing**: Convert multiple records into a format suitable for bulk operations

## Example Workflow

1. Fetch data from an API or database (returns array of objects)
2. Use this function to convert the array to CSV
3. Use the output variable to:
   - Upload to cloud storage
   - Send as an email attachment
   - Save to a file system
   - Pass to another service
