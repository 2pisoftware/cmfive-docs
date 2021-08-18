---
title: Writing Insight
layout: page
type: doc
---

## Writing Insight Classes

The insight module allows users to write insights that can be saved, exported, and run when needed.<br>
This page will go over the primary pieces of code that each insight needs to work correctly in all the above ways.

The insights class will be the sort of insight it is, followed by Insight (e.g. the audit insight is AuditInsight). All insights must extend Insight Base Class.

```php
class ExampleInsight extends InsightBaseClass
```

Below this, give the variables for the insights name and description. These will appear in the insight list, the first page seen in cmfive when you click on the insight module.

```php
public $name = "Example Insight";
public $description = "This insight is being used to show correct insight syntax in the docs";
```
These variables will indicate to users which isnight is which.

All insights will contain a getFilters function and a run function. The getFilters function will be called when a user clicks on the View button next to the insight. The run function is called when the user clicks Run from the view screen.

getFilters will be an array, which sets up the parameters the user can choose. Before viewing an insight, the user may specify it to only show information from specififc dates, for certain users, etc.<br>
Add the below code underneath your name and description variables.

```php
public function getFilters(Web $w, $parameters = []): array
{
```

The filters you choose for the user to select from will depend on the insight you are creating.<br>
The below code shows the code that goes in your getFilters function. It has filters for choosing the date to a from that the insight shows.

```php
    return [
                "Options" => [
                    [
                        [
                            "Date From", "date", "dt_from", array_key_exists('dt_from', $parameters) ? $parameters['dt_from'] : null
                        ],
                        [
                            "Date To", "date", "dt_to", array_key_exists('dt_to', $parameters) ? $parameters['dt_to'] : null
                        ],
                    ]
                ]
            ];
}
```

You will notice that both filters contain an array_key_exists function. This is required on all filters in your insight. When you click the Change Insight Parameters button, the options you chose that session previously will be prefilled for you.

The run function will also be an array. It will find data based on the selected filters and then organise it into the appropriate columns for each table in the insight.<br>
Place the below code under your getFilters function.

```php
public function run(Web $w, $parameters = []): array
{
```
First, the insight finds the correct data based on the filters you have chosen. The data variable for our Example Insight will look like the code below.

```php
$data = ExampleService::getInstance($w)->getExamples(($parameters['dt_from']), ($parameters['dt_to']));
```

The getExamples function refers to a where array. You will have to create one in the appropriate service class for your insight. It will have to cover all the filters in your getFilters function. The where array will handle the options the user selects when viewing an insight.

After retrieving the data based on the selected filters, your run function must build its table(s). It will look something like this.

```php
if (!$data) {
             $results[] = new InsightReportInterface('Example Report', ['Results'], [['No data returned for selections']]);
        } else {
            // convert $data from list of objects to array of values
            $convertedData = [];
            
            foreach ($data as $datarow) {
                $row = [];
                $row['Module'] = $datarow->module;
                $row['URL'] = $datarow->path;
                $row['Class'] = $datarow->db_class;
                $row['Action'] = $datarow->db_action;
                $row['DB_Id'] = $datarow->db_id;
                $convertedData[] = $row;
            }
             $results[] = new InsightReportInterface('Example Report', ['Module', 'URL', 'Class', 'Action', 'DB Id'], $convertedData);
        }
        return $results;
    }
}
```

The first few rows indicate what the insight will display if no data comes back.<br>
The rows below use the Insight Report Interface to build a table. Each of the rows are built using the where array in the service class. The column names and insight title are given below.<br> 
The above insight is titled Example Report. It contains the five columns: Module, URL, Class, Action, and DB Id.<br>
The function then returns the data in the table(s) as results.

## Notes on Export Requirements

There are a few brief things that need to be checked for the two export types.

For exporting to CSV, check that your first php tag in your insight is on line 1. Any empty space in your insight before it will create blank rows in exported CSV files.

When Exporting to PDF, you will be asked to select a template from a drop-down list. Templates can be created for your insights in the Admin module of cmfive.<br>
You will notice that only specific templates appear in the drop-down list. Your category must be the insight class, followed by _pdf, to make sure your template appears (This is the insight class readable by a computer, not the human-readable name.) Your templates category will be something like 'ExampleInsight_pdf'. This ensures that only templates created for PDF exports for the insight you are currently viewing are shown in the drop-down list.