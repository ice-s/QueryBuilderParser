# QueryBuilderParser

Status Label  | Status Value
--------------|-------------
Build | [![Build Status](https://travis-ci.org/timgws/QueryBuilderParser.svg?branch=master)](https://travis-ci.org/timgws/QueryBuilderParser)
Insights | [![SensioLabsInsight](https://insight.sensiolabs.com/projects/70403e01-ad39-4117-bdef-d0c09c382555/mini.png?branch=master)](https://insight.sensiolabs.com/projects/70403e01-ad39-4117-bdef-d0c09c382555)

**QueryBuilderParser** is designed mainly to be used inside Laravel projects, however it can be used outside Laravel
projects by using Illuminate/Database.

A simple to use query builder for the [jQuery QueryBuilder plugin](http://mistic100.github.io/jQuery-QueryBuilder/).

    use timgws\QueryBuilderParser;

    $table = DB::table('table_of_data_to_interegate');
    $qbp = new QueryBuilderParser(
        array( 'row1', 'row2', 'row3' )
    );

    $query = $qbp->parse($input['querybuilder'], $table);

    $rows = $query->get();
    return Response::JSON($rows);

Mixed with Datatables, this makes for some true awesome.

```php
    use timgws\QueryBuilderParser;
    
    class AdminUserController {
        function displayUserDatatable() {
            /* builder is POST'd by the datatable */
            $queryBuilderJSON = Input::get('builder');
            
            $show_columns = array('id', 'username', 'email_address');
            
            $query = new QueryBuilderParser($show_columns);
            
            /** Illuminate/Database/Query/Builder $queryBuilder **/
            $queryBuilder = $query->parse(DB::table('users'));
            
            return Datatable::query($queryBuilder)
                ->showColumns($show_columns)
                ->orderColumns($show_columns)
                ->searchColumns($show_columns) 
                ->make()
        }
    }
```
