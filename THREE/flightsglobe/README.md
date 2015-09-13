# FlightsGlobe: Mapping Flight Patterns from openflights.org to 3D Globe

Programming lanauges used here:
- Python
- JavaScript (three.js)

## Project Structure

```
three_js_globe/
├── dep_dest_to_json.py 		<<-- get lat/long from departure and destination from flights.csv
├── flight_data.json 			<<-- output produced by flights_csv_to_json.py
├── flight_data_dep_dest.json <<-- output produced by dep_dest_to_json.py
├── flights.csv 				<<-- file exported from cartodb
├── flights_csv_to_json.py 	<<-- get airport lat/long data from flights.csv
├── globe 					<<-- taken from https://github.com/dataarts/webgl-globe/#basic-usage
│   ├── globe.js  				
│   ├── globe_arcs.js 		<<-- from http://engineroom.trackmaven.com/blog/using-cartodb-and-threejs-for-mapping/
│   ├── world.jpg
│   └── world2.jpg
├── helpers
│   └── three.min.js
├── map.html
└── map_arcs.html             <<-- wip
``` 

## Steps Needed to Produce FlightsGlobe
1. **Export CSV file with flights data** (lat/long of departure and destination) from [cartodb/lingdp](https://lingdp.cartodb.com/tables/start_dest_points/public) (this data was downloaded for all Swiss International flights from the 14th of August 2015 from [openflights.org](www.openflights.org))
2. **Convert** `.csv` to `.json` format:
  - for only destination points: `$ python flights_csv_to_json.py`
    - This will produce the file `flight_data.json`
  - for destination and departure points: `$ python dep_dest_to_json.py`
    - This will produce the file `flight_data_dep_dest.json`

3. (If you run it from local server) Start e.g. Python SimpleHTTPServer: 
`$ python -m SimpleHTTPServer 8000`
4. Visit `localhost:8000` in e.g. Chrome Browser

## Credits
- https://github.com/dataarts/webgl-globe/#basic-usage (for `globe.js`)
- http://engineroom.trackmaven.com/blog/using-cartodb-and-threejs-for-mapping/ (tutorial on how to combine cartodb data with three.js; `globe_arcs.js`)
- http://p1.pichost.me/i/28/1509588.jpg (source for `world.jpg`)
- https://d3ui957tjb5bqd.cloudfront.net/images/screenshots/products/11/110/110839/007-world-map-o.jpg?1399919132 (source for `word2.jpg`)


