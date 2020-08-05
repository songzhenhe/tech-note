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




