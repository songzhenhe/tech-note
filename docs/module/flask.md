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







