Geospatial data in python
=============
geo modulus


Convert
----------------

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

