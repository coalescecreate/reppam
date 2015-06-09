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

	$(selector).reppam({countriesUrl: 'countries.json'});

#### urlParams ####

*Default* `{}`   
*Expects* `object`

Enter API key and other important information for the url parameters. [More information about using API keys here](https://developers.google.com/maps/documentation/javascript/tutorial)

	$(selector).reppam({countriesUrl: 'countries.json'});

#### mapOptions ####

*Default* `{}`   
*Expects* `object`

Options relating to the instantiation of google maps. Common usage includes [styles from the google maps styling wizard](http://gmaps-samples-v3.googlecode.com/svn/trunk/styledmaps/wizard/index.html) and background color to match the background color of the map. Optionally a no scroll if there is content after the map that the user needs to be able to get to. [All options for the mapOptions object are here](https://developers.google.com/maps/documentation/javascript/reference#MapOptions)

	$(selector).reppam({mapOptions: {}});

#### mapData ####

*Default* `'map-data.json'`   
*Expects* `string or object`

Relative link to a json file containing the following. isoCode is the two letter version i.e. Sweden is SE
	
	{
		currentLocation: [isoCode, country-name],
		locations: {
			id: {
				name: string,
				address: html,
				latitude: integer
				longitude: integer
			},
			id ...
		},
		countries: {
			isoCode: {
				id: isoCode,
				country: string,
				sw: {lat: integer,lng: integer},
				ne: {lat: integer,lng: integer}
			}
		}
	}

Countries are so that map can be focused on the country your IP originates from. This is a method of caching for Google's geocoder. All values come from there. For a faster more compact version of this plugin the object data can be added directly to this property instead of being ajaxed in. Especially useful for maps with only a couple of markers.

	$(selector).reppam({mapData: 'map-data.json'});

#### defaultCountry ####

*Default* `false`   
*Expects* `false or ISO country code`

If there are no markers to display in the country that the user comes from. This country will be then shown.

	$(selector).reppam({countriesUrl: 'countries.json'});

#### startPosition ####

*Default* `false`   
*Expects* `false or object`

This will override any other automatic actions. If the map is to be focussed on a particular spot no matter the user. Object uses three properties. Zoom an integer between 3-21, lat an integer between -90 and 90, lng an integer between -90 and 90.

	$(selector).reppam({startPosition: false});

#### useMarkerClusterer ####

*Default* `true`   
*Expects* `boolean`

Use this only if you want to include a map that doesn't use the markerclusterer library but that has the library installed.

	$(selector).reppam({useMarkerClusterer: false});

#### multipleMarker ####

*Default* `false`   
*Expects* `false, object`

An object describing the icon. [More information regarding this is further down the page.](#icons)

	$(selector).reppam({multipleMarker: false});

#### singleMarker ####

*Default* `false`   
*Expects* `false, object`

An object describing the icon. [More information regarding this is further down the page.](#icons)

	$(selector).reppam({singleMarker: false});

#### personMarker ####

*Default* `false`   
*Expects* `false, object`

An object describing the icon. [More information regarding this is further down the page.](#icons)

	$(selector).reppam({singleMarker: false});

#### zoomedIn ####

*Default* `14`   
*Expects* `integer 0-21`

The zoom level on google maps for zooming in on a specific marker. The higher the number the higher the zoom.

	$(selector).reppam({zoomedIn: 14});

#### strokeColor ####

*Default* `#000000`   
*Expects* `CSS3 color code except extended color names`

The line color between current location and nearest store. Line drawn is 3px wide.

	$(selector).reppam({strokeColor: '#000000'});


#### Classes ####

Numerous classes can be reassigned. Check the `defaultOpts {} as to which classes are able to be manipulated.


### Icons ###

#### url ####

*Default* `default built in markers`   
*Expects* `string`  
*Available For* `All`

The url of the map icon. This can be a sprite and in any CSS accepted format.

	$(selector).reppam(singleMarker: {
		url: 'sprite.png'
	});

#### size ####

*Default* `size of image from url`   
*Expects* `array`  
*Available For* `All`

Size of the icon. This must be submitted if using a sprite otherwise the whole sprite will be visible. The array requires x by y an array of integers. The integers are interpreted as pixel values only.

	$(selector).reppam(singleMarker: {
		size: [32,50]
	});

#### anchor ####

*Default* `bottom middle of size`   
*Expects* `array`  
*Available For* `All`

This marks the position of where the icon should "touch the ground". The sizing is relative to the size of the icon. The distance is worked out from the top left of the image which is 0,0 and counted to the right and down.

	$(selector).reppam(singleMarker: {
		anchor: [16,50]
	});

#### origin ####

*Default* `0,0`   
*Expects* `array`  
*Available For* `All`

Specifically used for sprites. Defines where the marker's start point is for the size. Position of the icon is taken from the top left and is counted to the right and down.

	$(selector).reppam(singleMarker: {
		anchor: [32,0]
	});

#### scaledSize ####

*Default* `size of image from url`   
*Expects* `array`  
*Available For* `singleMarker,personMarker`

Size of the icon before scaling. 

	$(selector).reppam(singleMarker: {
		scaledSize: [64,100]
	});

#### fontFamily, fontStyle, fontWeight, textColor, textDecoration, textSize ####

*Default* `arial sans-serif, normal, bold, black, none, 11`  
*Expects* `string`  
*Available For* `multipleMarker`

Font styling for numbers of collections of markers. Multiple markers are used for the clusterer and these numbers show how many markers are defined by that marker.

	$(selector).reppam(singleMarker: {
		fontFamily: 'times serif', 
		fontStyle: 'italic', 
		fontWeight: 'normal', 
		textColor: '#330002', 
		textDecoration: 'underline', 
		textSize: 14
	});

#### anchorText ####

*Default* `middle`  
*Expects* `array`  
*Available For* `multipleMarker`

Position of the text from the center of the icon to the center of the text. For positioning the text.

	$(selector).reppam(singleMarker: {
		anchorText: [0,0]
	});


### Actions ###

#### #locate-me ####

Clicking a selector with the id locate-me will trigger the map to add a marker on the map of the current position of the user using HTML5 geolocation.

#### #nearest ####

Clicking a selector with the id locate-me will trigger the map to add a marker on the map of the current position of the user using HTML5 geolocation and find the nearest marker to the user. If the marker is in the range of 100km the user's marker and the closest marker will be shown on the map otherwise the map will zoom in to the nearest marker. Between the markers a line is drawn. The line is a geodesic line connecting the two points to color this line use strokeColor.


### Methods ###

#### showOnMap ####

*Expects* `object with id of listing and optionally a callback`

Send the ID of the listing to show the marker on the map. The zoomedIn properties will be used to zoom in on that marker.

	$(selector).reppam('showOnMap', {
		id: idOfListing,
		callback: function(response) {
			//Response is an object that returns true/false
		}
	});

#### showCoords ####

*Expects* `object with lat, lng, zoom and optionally a callback`

Send all the coords to zoom in on a specific area of the map. Expects an object that describes the latitude, longitude and zoom level of the map.

	$(selector).reppam('showOnMap', {
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

**Version 0.3.1**  
Parsed start data into integers.

**Version 0.3.0**  
Updated documentation to reflect latest changes. Enabled user to put in a start position and pass an object in to the mapData instead of linking to a json file.

**Version 0.2.0**  
Updates for better integration. Still needs documentation on some of the newer features.

**Version 0.1.0**  
Initial commit


### Development ###

**Requirements**
* This plugin requires [node](http://nodejs.org/), [gulpjs](http://gulpjs.com/) and [bower](http://bower.io/).
* Follow JSCS guidelines a styling-example.js is also included.
* Run `bower install` and `npm install` to get dev dependencies. Bower and Gulp is assumed to be running globally.

### Contact ###

This is a small plugin by [Young/Skilled](http://youngskilled.com).   
Contact [richard](mailto:richard@youngskilled) for more details about this plugin.