# overpasser
Fluid Java interface to [OpenStreetMap](https://www.openstreetmap.org/) data through querying the [Overpass API](http://wiki.openstreetmap.org/wiki/Overpass_API). No more query string forging by hand!

### Example code
An Overpass query like this:
```
["out":"json"]["timeout":"30"];
(
    node
        ["amenity"="parking"]
        ["access"!="private"]
        (47.48047027491862,19.039797484874725,47.51331674014172,19.07404761761427);
        <;
);
out body center qt 100;
```

...can be expressed like:
```java
String query = new OverpassQuery()
        .format(JSON)
        .timeout(30)
        .mapQuery()
            .node()
            .amenity("parking")
            .notEquals("access", "private")
            .boundingBox(
                47.48047027491862, 19.039797484874725,
                47.51331674014172, 19.07404761761427
            )
        .end()
        .output(OutputVerbosity.BODY, OutputModificator.CENTER, OutputOrder.QT, 100)
        .build()
;
```

...or you can just use ```.output(100)``` at the end to use the defaults.

### Language support
* Settings
  * [output format](http://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL#Output_Format_.28out.29) - currently JSON only
  * [timeout](http://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL#timeout)
  * [output parameters](http://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL#Print_.28out.29) - verbosity, modificators, sort order
* [Filters](http://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL#Filters)
  * standalone filter 
  * exact filter matching by value (and negation)
  * regex filter matching by value (and negation)
  * multiple values
* Map queries
  * selecting nodes
  * setting [bounding box](http://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL#Bounding_box)
  
### Modules
* [library](https://github.com/zsoltk/overpasser/tree/master/library) - Core functionality in a standalone module: only Java dependencies
* [library-retrofit-adapter](https://github.com/zsoltk/overpasser/tree/master/library-retrofit-adapter) - [Retrofit](http://square.github.io/retrofit/) adapter towards the overpass-api server
* [sample](https://github.com/zsoltk/overpasser/tree/master/sample) - An Android sample using both of the above

![](http://imgur.com/A4TGjjx.png)

### Download

The library and the retrofit adapter are available on [Maven Central](http://search.maven.org/#search%7Cga%7C1%7Coverpasser). You can find them with [Gradle, please](http://gradleplease.appspot.com/#overpasser) too, or just use these gradle dependencies:

Library:
```groovy
dependencies {
    compile 'hu.supercluster:overpasser:0.1.0'
}
```
  
Retrofit adapter:
```groovy
dependencies {
    compile 'hu.supercluster:overpasser-retrofit-adapter:0.1.0'
}
```

**Please note**: This is not a production ready library. Use it at your own risk.


### License

    Copyright 2015 Zsolt Kocsi

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
