# maptalks.three

[![CircleCI](https://circleci.com/gh/maptalks/maptalks.three/tree/master.svg?style=shield)](https://circleci.com/gh/maptalks/maptalks.three)
[![NPM Version](https://img.shields.io/npm/v/maptalks.three.svg)](https://github.com/maptalks/maptalks.three)

A maptalks Layer to render with THREE.js

![screenshot](https://cloud.githubusercontent.com/assets/13678919/26443408/db7afe66-416a-11e7-951b-0f99beaadb5a.jpg)
## Examples

* [Extrude Buildings](https://maptalks.github.io/maptalks.three/demo/buildings.html).
* [Load MTL Model](https://maptalks.github.io/maptalks.three/demo/obj.html).

## Install
  
* Install with npm: ```npm install maptalks.three```. 
* Download from [dist directory](https://github.com/maptalks/maptalks.three/tree/gh-pages/dist).
* Use unpkg CDN: `https://unpkg.com/maptalks.three/dist/maptalks.three.min.js`

## Usage

As a plugin, `maptalks.three` must be loaded after `maptalks.js` and `THREE.js` in browsers.
```html
<script type="text/javascript" src="https://unpkg.com/three@0.84.0/build/three.min.js"></script>
<script type="text/javascript" src="https://unpkg.com/maptalks/dist/maptalks.min.js"></script>
<script type="text/javascript" src="https://unpkg.com/maptalks.three/dist/maptalks.three.js"></script>
<script>
var threeLayer = new maptalks.ThreeLayer('t');
threeLayer.prepareToDraw = function (gl, scene, camera) {
    var light = new THREE.PointLight(0xffffff, 0.8);
    camera.add(light);
    var me = this;
    countries.features.forEach(function (g) {
        var num = g.properties.population;
        var color = getColor(num);

        var m = new THREE.MeshPhongMaterial({color: color, opacity : 0.7});

        var mesh = me.toExtrudeGeometry(maptalks.GeoJSON.toGeometry(g), num / 4E2, m);
        if (Array.isArray(mesh)) {
            scene.add.apply(scene, mesh);
        } else {
            scene.add(mesh);
        }
    });
};

map.addLayer(threeLayer);
</script>
```

With ES Modules:

```javascript
import * as maptalks from 'maptalks';
import { ThreeLayer } from 'maptalks.three';

const map = new maptalks.Map('map', { /* options */ });

const threeLayer = new ThreeLayer('t');
threeLayer.prepareToDraw = function (gl, scene, camera) {
    var light = new THREE.PointLight(0xffffff, 0.8);
    //...
};

threeLayer.addTo(map);
```

## Supported Browsers

IE 11, Chrome, Firefox, other modern and mobile browsers that support WebGL;

## API Reference

```ThreeLayer``` is a subclass of [maptalks.CanvasLayer](http://maptalks.github.io/docs/api/CanvasLayer.html) and inherits all the methods of its parent.

### `Constructor`

```javascript
new maptalks.ThreeLayer(id, options)
```

* id **String** layer id
* options **Object** options
    * glOptions **Object** options when creating webgl context, null by default
    * doubleBuffer **Boolean** whether the layer canvas is painted with double buffer, true by default
    * Other options defined in [maptalks.CanvasLayer](http://maptalks.github.io/docs/api/CanvasLayer.html)

## Contributing

We welcome any kind of contributions including issue reportings, pull requests, documentation corrections, feature requests and any other helps.

## Develop

The only source file is ```index.js```.

It is written in ES6, transpiled by [babel](https://babeljs.io/) and tested with [mocha](https://mochajs.org) and [expect.js](https://github.com/Automattic/expect.js).

### Scripts

* Install dependencies
```shell
$ npm install
```

* Watch source changes and generate runnable bundle repeatedly
```shell
$ gulp watch
```

* Tests
```shell
$ npm test
```

* Watch source changes and run tests repeatedly
```shell
$ gulp tdd
```

* Package and generate minified bundles to dist directory
```shell
$ gulp minify
```

* Lint
```shell
$ npm run lint
```
