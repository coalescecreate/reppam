# Reppam - An abstraction layer for Google Maps V3 #

A jQuery plugin to display points on Google maps, get directions between current position and where you are now, which is the closest point. This is just an abstraction layer for Google Maps API V3. Use in conjunction with markerclusterplus for better marker control when using more markers.

## Functions included are: ##

* Support for [markerclusterplus](http://google-maps-utility-library-v3.googlecode.com/svn/trunk/markerclustererplus/docs/reference.html) groups markers at different zoom levels.
* Click on a marker shows an infowindow with content. 
	* Click again on the marker zooms in to predfined level.
* Show my position. Adds a marker as to where you are on the map and centers you at that zoom level.
* Show closest store. Connects a line between your marker and the closest store.
	* Within 100kms shows marker and store.
	* Over 100kms zooms in on store.
	* Click on the line shows both marker and store.


### Usage ###


Initiate with `$(selector).reppam({'some':'property'});`   
Invoke methods with `$(selector).reppam('method', {'some':'property'});`   
Example

	$('.reppam').reppam({
		debug: true,
		mapsURL: '//maps.google.com/maps/api/js'
	})

### HTML ###

Following structure is required for selector to work. (Using Emmet tab complete for full HTML or check /dev/index.html)

	div.reppam

### Properties ###

#### mapsURL ####

*Default* `'//maps.google.com/maps/api/js'`   
*Expects* `string`

Link to google maps API. Use in conjuction with urlParams to automatically get google maps url.

	$(selector).redils({countriesUrl: 'countries.json'});

#### urlParams ####

*Default* `{}`   
*Expects* `object`

Enter API key and other important information for the url parameters. [More information about using API keys here](https://developers.google.com/maps/documentation/javascript/tutorial)

	$(selector).redils({countriesUrl: 'countries.json'});

#### countriesUrl ####

*Default* `'countries.json'`   
*Expects* `string`

Relative link to a json file containing country bounds so that map can be focused on the country your IP originates from. This is a method of caching for Google's geocoder. All values come from there.

	$(selector).redils({countriesUrl: 'countries.json'});

#### markersUrl ####

*Default* `'markers.json'`   
*Expects* `string`

Relative link to a json file containing information about all the markers. An id, name, latitude, longitude and content are used to show markers on the map. This also has an array for current location.

	$(selector).redils({countriesUrl: 'countries.json'});

#### defaultCountry ####

*Default* `false`   
*Expects* `false or ISO country code`

If there are no markers to display in the country that the user comes from. This country will be then shown.

	$(selector).redils({countriesUrl: 'countries.json'});

#### multipleMarker ####

*Default* `{}`   
*Expects* `object`

An object describing the icon. This object is specific to markerclusterplus and that library needs to be loaded for this to be valid. [More information regarding specific values for the icon is here.](http://google-maps-utility-library-v3.googlecode.com/svn/trunk/markerclustererplus/docs/reference.html)

	$(selector).redils({multipleMarker: {}});

#### singleMarker ####

*Default* `{}`   
*Expects* `object`

An object describing the icon. This object is specific to google maps Marker method for the icon property. [More information regarding specific values for the icon is here.](https://developers.google.com/maps/documentation/javascript/reference#MarkerOptions)

	$(selector).redils({singleMarker: {}});

#### personMarker ####

*Default* `{}`   
*Expects* `object`

personMarker is specifically used to show the current location of the user. An object describing the icon. This object is specific to google maps Marker method for the icon property. [More information regarding specific values for the icon is here.](https://developers.google.com/maps/documentation/javascript/reference#MarkerOptions)

	$(selector).redils({singleMarker: {}});

#### zoomedIn ####

*Default* `14`   
*Expects* `integer 0-21`

The zoom level on google maps for zooming in on a specific marker. The higher the number the higher the zoom.

	$(selector).redils({zoomedIn: 14});

#### strokeColor ####

*Default* `#000000`   
*Expects* `CSS3 color code except extended color names`

The line color between current location and nearest store. Line drawn is 3px wide.

	$(selector).redils({strokeColor: '#000000'});


#### Classes ####

Numerous classes can be reassigned. Check the `defaultOpts {} as to which classes are able to be manipulated.


### Methods ###

#### showOnMap ####

*Expects* `object with id of listing and optionally a callback`

Send the ID of the listing to show the marker on the map. The zoomedIn properties will be used to zoom in on that marker.

	$(selector).redils('showOnMap', {
		id: idOfListing,
		callback: function(response) {
			//Response is an object that returns true/false
		}
	});

#### showCoords ####

*Expects* `object with lat, lng, zoom and optionally a callback`

Send all the coords to zoom in on a specific area of the map. Expects an object that describes the latitude, longitude and zoom level of the map.

	$(selector).redils('showOnMap', {
		lat: latitude, //(integer between 90 and -90)
		lng: longitude, //(integer between 90 and -90)
		zoom: 14, //(intger between 0 and 21)
		callback: function(response) {
			//Response is an object that returns true/false
		}
	});


### Roadmap ###

* Option to expand bounds to show initial countryand then the nearest store to that country.
* Show info window when using method show on map - needs to have markers as a global plugin object.
* Add distance to info windows when show nearest store has been used.
* Show next closest store.


### Changelog ###

**Version 0.1**  
Initial commit


### Development ###

**Requirements**
* This plugin requires [node](http://nodejs.org/), [gulpjs](http://gulpjs.com/) and [bower](http://bower.io/).
* Follow JSCS guidelines a styling-example.js is also included.
* Run `bower install` and `npm install` to get dev dependencies. Bower and Gulp is assumed to be running globally.

### Contact ###

This is a small plugin by Young Skilled.
Contact [richard](mailto:richard@youngskilled) for more details about this plugin.