## SQLFlow

SQLFlow is a tool that automates data lineage discovery by analyzing the SQL script.
It generates a nice clean diagram to show the dataflow among the table/view and columns
in the data warehouse.

Support more than 20 major databases including bigquery, couchbase, dax, db2, 
greenplum, hana, hive, impala, informix, mdx, mysql, netezza, openedge, oracle, postgresql, 
redshift, snowflake, sqlserver, sybase, teradata, vertica,

Just paste the SQL script and click a button, you will get the data lineage diagram instantly,
highlight the dataflow in the diagram with a simple mouse click.

You can also call the RESTful API provided by this tool in your own program and 
get the data lineage and diagram model information in a JSON snippet to make further usage.

### [SQLFlow Live](https://www.gudusoft.com/sqlflow)


![SQLFlow architecture](sqlflow_architecture.png)

### SQLFlow components 
![SQLFlow components](sqlflow_components.png)

### SQLFlow

#### SQLFlow frontend
1. Send the SQL script received from the browser in JSON to the backend.

2. After receiving the result which includes the data lineage and diagram model 
generated by the backend, visualize the diagram model in the browser.

3. Highlight the dataflow in the diagram when the user clicks on a specific column.

#### SQLFlow backend
1. `FlowAnalyzer`: receiving the SQL script from the frontend and parse the SQL script into parse tree nodes
by utilizing [the GSP library](http://www.sqlparser.com), then calculate the data lineage by analyzing AST.

	The `FlowAnalyzer` component is open source and can be executed as a standalone tool. Take SQL text
	as input and generate data lineage in JSON format. Check [`FlowAnalyzer`](https://github.com/sqlparser/gsp_demo_java/tree/master/src/main/java/demos/dlineage) for more.

2. `FlowLayout`:  Calculating the layout of database objects(table/column) in the dlineage and 
 generate the diagram model with all necessary position data, including nodes and edges.
 `FlowLayout` depends on `doLayout library` to layout the database objects.

3. Return a JSON snippet including the data lineage and diagram model to the frontend.



### Use SQLFlow in your flavor ways

#### 1. Visit gudusoft.com website using browser
	You may paste your SQL script into the SQLFlow web page, or upload the SQL file to the site.
	select the correct database and then click the visualize button.

#### 2. Use RESTFul APIs
	SQLFlow provides RESTful API, so your program can communicate with the SQLFlow backend directly.
	Sending the SQL to SQLFlow backend and receive a JSON snippet including the data lineage and diagram model
	for further processing in your own program.

	[SQLFlow RESTful API Online](https://api.gudusoft.com/gspLive_backend/swagger-ui.html#!/sqlflow-controller/generateSqlflowUsingPOST) [C# Demo](https://github.com/sqlparser/sqlflow_public/tree/master/api/client/csharp)

	Please put the following authorization code in your request header when calling the RESTful API.

	```json
	Authorization: token eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJndWVzdFVzZXIiLCJleHAiOjE1ODEyMDY0MDAsImlhdCI6MTU3MzQzMDQwMH0.-lvxaPlXmHbtgSFgW7ycu8KUczRiFZy5A1aNRGY-tKM
	```

#### 3. Add visualize feature in your own application/website
	The SQLFlow consists of the frontend and backend. 
	You may setup the frontend on you own web server, or include the frontend in your application to add visualize feature.

	Your application still need connect to the SQLFlow backend in order to process the SQL code to get data lineage.

#### 4. Install both frontend and backend on your own application/server
	Setup both the frontend and backend of SQLFlow on our server. 

	Please check the [setup manual](install_sqlflow.md).

	In order to setup SQLFlow on your own server, Please contact us (support@gudusoft.com) to obtain a commerical license to get all those distribution files.
	Please note that the distribution files doesn’t include the source code of the SQLFlow except the `FlowAnalyzer` which is [open source here](https://github.com/sqlparser/gsp_demo_java/tree/master/src/main/java/demos/dlineage).


### [sqlflow relations](dbobjects_relationship.md)
The relationship between column and column, column and table/view.
One relation includes one target column and a relationship type and one or more source columns.

