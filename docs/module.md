# Plotly & Dash

Dashboard


## Plotly
 

Embedding a Dash app within an Existing Flask App
As discussed in the Deployment Chapter, Dash uses the Flask web framework under the hood. 
This makes it fairly straightforward to embed a Dash app at a specific route of an existing Flask app.



In the following example, a Dash app is mounted at the /dash route (eg http://localhost:8050/dash) of a Flask app:

``` python
import flask
import dash
import dash_html_components as html

server = flask.Flask(__name__)

@server.route('/')
def index():
    return 'Hello Flask app'

app = dash.Dash(
    __name__,
    server=server,
    routes_pathname_prefix='/dash/'
)

app.layout = html.Div("My Dash app")

if __name__ == '__main__':
    app.run_server(debug=True)

``` python

Note: it is important to set the name parameter of the Dash instance to the value __name__, 
so that Dash can correctly detect the location of any static assets inside an assets directory for this Dash app.





## use selected column in Dash DataTable

``
#         
columns=[{'name': i, 'id': i} for i in df.loc[:,['Magnitude','Latitude','Longitude','Time', 'Place', 'Detail']]],
#        fixed_rows={ 'headers': True, 'data': 0 },
        data=df.iloc[:,[1,4,5,6,0,3]].to_dict('records')
````



```
def create_table(df):
    #format dataframe column of urls so that it displays as hyperlink
    def display_links(df):
        links = df['Detail'].to_list()
        rows = []
        for x in links:
            link = '[Geojson](' +str(x) + ')'
            rows.append(link)
        return rows
    
    df['Detail'] = display_links(df)


    table = dash_table.DataTable(
        id='cust-table',
#        columns=[{"name": i, "id": i} for i in df.columns],
        columns=[{'name': 'Magnitude', 'id':'Magnitude'}, 
                 {'name': 'Latitude', 'id':'Latitude'}, 
                 {'name': 'Longitude', 'id':'Longitude'}, 
                 {'name': 'Time', 'id':'Time'}, 
                 {'name': 'Depth', 'id':'Depth'}, 
                 {'name': 'Place', 'id':'Place'},
                 {'name': 'Detail', 'id':'Detail','type':'text','presentation':'markdown'}
        ],
#        columns=[{'name': i, 'id': i} for i in df.loc[:,['Magnitude','Latitude','Longitude','Time','Depth','Place','Detail']]],
#        fixed_rows={ 'headers': True, 'data': 0 },
#        data=df.to_dict('records'),
        data=df.iloc[:,[1,4,5,2,6,0,3]].to_dict('records')
    )
    return table
```





# Flask

Flask's setup is merely a copy+paste of the following five lines:

``` python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"
```

``` python
from flask import Flask

app = Flask(__name__,
            instance_relative_config=False,
            template_folder="templates",
            static_folder="static")
```

`Markup` allows us to return an HTML page by rendering a string as HTML:
```
from flask import Flask, Markup
app = Flask(__name__)

@app.route("/")
def hello():
    return Markup("<h1>Hello World!</h1>")
```


`return_template` will return an HTML page by finding the page in our /templates folder:
```
from flask import Flask, render_template
app = Flask(__name__, template_folder="templates")

@app.route("/")
def hello():
    return render_template("index.html")
```

`make_response` has a number of uses, the most notable of which is to serve a response in the form of a JSON object. 
If our application is an API, we'd return a response objects instead of pages:

On the topic of creating APIs with Flask, we can also specify whether the route at hand is a POST, GET, or some other method. 
This is handled easily within the route decorator:

```
from flask import Flask, make_response, request
app = Flask(__name__)

@app.route("/", methods=['GET'])
def hello():
    if request.method != 'GET':
        return make_response('Malformed request', 400)
    headers = {"Content-Type": "application/json"}
    return make_response('it worked!', 200, headers)
```


```
from flask import Flask, make_response, request, jsonify
app = Flask(__name__)

@app.route("/", methods=['GET'])
def hello():
    if request.method != 'GET':
        return make_response('Malformed request', 400)
    my_dict = {'key': 'dictionary value'}
    headers = {"Content-Type": "application/json"}
    return make_response(jsonify(my_dict), 200, headers)
```








# Geospatial data in python

geo modulus


## Convert


simplekml module.

Example:

The simplekml newpoint method requires that we send it a NAME and a COORDS, each of which we can easily pull directly from the CSV file that we’ve opened via our csv reader. Because csv.reader returns a list, we can access elements of that list by their numerical index. For the first row of our CSV file, row[0] refers to “Charleston County, SC”, and row[1] refers to 32.7956561.

We saved our coordinates as lat,long but simplekml wants them in the reverse order (long, lat), which is why we need to create the list like [(row[2],row[1])] as seen above.

So for each row in our CSV file, we create new point via the newpoint method of the kml object. Once we’ve finished with the file, we just need to call the save method on the kml object, and it will create a perfect KML file (‘battleplaces.kml’) for us.
```
import csv
import simplekml

inputfile = csv.reader(open('geocoded-placenames.csv','r'))
kml=simplekml.Kml()

for row in inputfile:
  kml.newpoint(name=row[0], coords=[(row[2],row[1])])

kml.save('battleplaces.kml')
```


# Pandoc

Convert document formats


## Convert
 
mkdocs new my-project
mkdocs build
mkdocs serve
mkdocs gh-deploy

GitHub Action 
A token is generated on your user account and a secret is part of the repository settings.
# Pandas

This document is for tips using pandas


## pd.read_csv


To keep the first row 0 (as the header) and then skip everything else up to row 10, you can write:
```
pd.read_csv('test.csv', sep='|', skiprows=range(1, 10))
```

Read all lines as values (no header, defaults to integers)
```
pd.read_csv(f, header=None)
```


Use a particular row as the header (skip all lines before that):
```
pd.read_csv(f, header=3)
```

Use a multiple rows as the header creating a MultiIndex (skip all lines before the last specified header line):
```
pd.read_csv(f, header=[2, 4]
```

Skip N rows from the start of the file (the first row that's not skipped is the header):
```
pd.read_csv(f, skiprows=3)   
```

Skip one or more rows by giving the row indices (the first row that's not skipped is the header):
```
pd.read_csv(f, skiprows=[2, 4])  
```








The iloc indexer syntax is data.iloc[<row selection>, <column selection>], which is sure to be a source of confusion for R users. 
“iloc” in pandas is used to select rows and columns by number, in the order that they appear in the data frame. 
You can imagine that each row has a row number from 0 to the total rows (data.shape[0])  and iloc[] allows selections based on these numbers. 
The same applies for columns (ranging from 0 to data.shape[1] )


# Single selections using iloc and DataFrame
# Rows:
data.iloc[0] # first row of data frame (Aleshia Tomkiewicz) - Note a Series data type output.
data.iloc[1] # second row of data frame (Evan Zigomalas)
data.iloc[-1] # last row of data frame (Mi Richan)
# Columns:
data.iloc[:,0] # first column of data frame (first_name)
data.iloc[:,1] # second column of data frame (last_name)
data.iloc[:,-1] # last column of data frame (id)


# Multiple row and column selections using iloc and DataFrame
data.iloc[0:5] # first five rows of dataframe
data.iloc[:, 0:2] # first two columns of data frame with all rows
data.iloc[[0,3,6,24], [0,5,6]] # 1st, 4th, 7th, 25th row + 1st 6th 7th columns.
data.iloc[0:5, 5:8] # first 5 rows and 5th, 6th, 7th columns of data frame (county -> phone1).






pandas.unique
pandas.drop

read into one dataframe
df_allraw =  pd.concat(pd.read_excel("cpt.xls", sheet_name=None), ignore_index=True)

read in as dictionary
allraw = pd.read_excel("cpt.xls", sheet_name=None)


import pandas as pd
all_dfs = pd.read_excel(workbook_url, sheet_name=None)
all_dfs.keys()
all_dfs['Sheet1'].head()



list(newdict.keys()).

# Pandoc

Convert document formats


## Convert
 

readme.md to readme.rst.
```
pandoc readme.md --from markdown --to rst -s -o readme.rst
```

convert multiple rst files to markdown (windows)
```
for %F in (*.rst) do pandoc %F --from rst --to markdown -s -o %F.md
```

