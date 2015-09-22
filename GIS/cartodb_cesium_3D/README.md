# 3D globe mapping with cartodb and cesium

Visualization that shows openflights.org data for Swiss International Airlines (only for 14th of August 2015) mapped on cartodb layer, plotted on a cesium 3D globe.


## Sources
- openflights.org for flights data (latitude/longitude data needed for plotting)
- http://bl.ocks.org/Xatpy/raw/854297419bd7eb3421d0/ for chosing cartodb maps base-layer
- cesium-cartodb pluging (https://github.com/CartoDB/cesium-cartodb): to allow import of cartodb map & data
- map/data from cartodb: I used this one: https://lingdp.cartodb.com/viz/c5004e0e-4403-11e5-80d1-0e853d047bba/map

## From cesium-cartodb repo:

### Installation

You can use `.../src/cesium-cartodb.js` as is or run `grunt build` to get a minified version `.../build/cesium-cartodb.min.js`. You must include either after including Cesium in your html.

```html
<script src="<path_to>/Cesium.js"></script>
<script src="<path_to>/cesium-cartodb.min.js"></script>
```

### Usage

After this, you can create new imagery objects in Cesium and use them as needed. `CartoDBImageryProvider` is derived from [Cesium's OpenStreetMap imagery provider](http://cesiumjs.org/Cesium/Build/Documentation/OpenStreetMapImageryProvider.html), and can be initialized and used just the same.

#### Basemap layer

Just add a `CartoDBImageryProvider` instance to a viewer in order to use CartoDB's basemaps in Cesium.

```js
var basemapProvider = new Cesium.CartoDBImageryProvider({
    url: '<MAP_TEMPLATE_URL>', // e.g.: http://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png,
    credit: 'Basemap courtesy of CartoDB'
});
var viewer = new Cesium.Viewer('cesiumContainer', {
    imageryProvider: basemapProvider,
    baseLayerPicker: false,
    fullscreenButton: false,
    homeButton: false,
    timeline: false,
    navigationHelpButton: false,
    animation: false,
    scene3DOnly: true,
    geocoder: false
});
```

#### Data layer

In order to have a data layer from tiles generated in CartoDB, use cartodb.core.js's getTiles to inject the tiles in Cesium.

```js
var layerData = {
    user_name: '<USER_NAME',
    sublayers: [{
        sql: "<SQL_QUERY>",
        cartocss: '<CARTOCSS>'
    }]
};
cartodb.Tiles.getTiles(layerData, function (tiles, err) {
    if (tiles == null) {
        console.log("error: ", err.errors.join('\n'));
        return;
    }
    viewer.scene.imageryLayers.addImageryProvider(new Cesium.CartoDBImageryProvider({
        url: tiles.tiles[0],
        credit: 'Data courtesy of CartoDB'
    }));
});
```