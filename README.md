#Google Map for Rose-Hulman

This macro (InteractiveMap.cshtml) contains the [Google Map API JavaScript v3](https://developers.google.com/maps/faq) to render an interactive campus map for the Rose-Hulman.edu Website.

This documentation consists of resources, data structure and flow, and the defined functions for initializing the map. There are many tools and resources available to continue the customization of this map. Please use the resources below for more details.

##Categories

1. Academics - Red
2. Arts - Blue
3. Athletics - Green
4. Parking - Black "P"
5. Administrative - Grey
6. Student Life - Purple

##Resources
The following is a list of resources for the API documentation, key and information to login to the API console:

* API Console & Reporting: https://code.google.com/apis/console
* API Documentation: https://developers.google.com/maps/documentation/javascript/tutorial 
* Latitude/Longitude Finder: http://itouchmap.com/latlong.html

##Structure
The data structure follows below:

1. Button Controls - Calling `toggleMarkers('CAT_ID')`
2. Container div with ID (map) - define width and height
3. API Script
4. InfoBox Script (/scripts/interactive-campus-map/campusMapOther.js)
5. Map Initialization (see "Functions" for more details)
	* Marker Locations
	* Map Styles
	* Info Window
	* Marker Initialization
	* Show/Hide Category
	* Initialize

##Variables

* Map - defines the map, used throughout
* RoseHulman - defines the center of the map
* gMarkers - Array, for pulling in the data used for the user buttons
* Marker, I, icon, image - all used for marker creation.
* Academics, arts, athletics, park, admin, studentLife - icons for the respective marker types
	* Located in the media library -> Design -> Interactive Campus Map
* Locations - array for the locations, used in `setMarkerLocations()`
* Current - utilized to store the current selected infoBox, to force one open at a time. Used in `defineInfoWindow()`

##Functions

The functions defined for this initial phase of the campus map are defined below:

###setMarkerLocations()
Defines a list of locations in an array, everything in the array is stored as a string. HTML is permitted in the description area. NOTE: The longitude is first, latitude is second.

	Locations = [
		{"id":"idNum",
		"category":"1-6 (see note above)",
		"campus_location":"As defined by printable campus map",
		"title":"Item Title",
		"description":"<p>Short location description. HTML is okay here to break up the content!</p>",
		"image":"/media/NUMBER/PathToFile.ext",
		"longitude":"See resources for how to find",
		"latitude":"See resources for how to find"
		}, {NEXT ITEM HERE}
	];

###setMapStyles()
Sets custom map styles using the styles array built into the API. See [Google Maps documentation](https://developers.google.com/maps/documentation/javascript/styling).
Also defines which maps are available for choice, within MapTypeControlOptions.

###defineInfoWindow(marker)
Uses the InfoBox.js class to customize the infoWindow. This function currently contains the old InfoWindow code from Google, but is not currently utilized.

This function is called within `MarkerInitialize()` to create the windows. Uses marker to create the HTML necessary to fill the box, also calls `hasImage(marker)` to determine if an image exists.

###hasImage(marker)
Determines whether a location has an image to display, does so if it exists. Otherwise returns nothing.

###markerInitialize()
Defines each marker by running through each iteration of location. Also uses a switch statement to determine which category and icon to use. This object can be defined with whatever information you wish. In this example, you CANNOT use campus_location in any other function, as it is not a defined object of marker. If you want to use an item within another function, it MUST be defined here.

	marker = new google.maps.Marker({
		// Marker Position
		position: new google.maps.LatLng(locations[i].latitude, locations[i].longitude),
		title: locations[i].title, // Marker Title
		icon: icon, // Which icon
		map:map, // what map
		category: locations[i].category, // what category
		animation: google.maps.Animation.DROP, // drop animation, bounce is also available
		image:locations[i].image, // image location
		description: locations[i].description, // description
		id: locations[i].id // location ID
	});

Calls `defineInfoWindow(marker)` to create the information windows. Also pushes marker details to gMarkers array for show/hide functionality.

###showAll()
For loop to set ALL items in gMarkers to show on the map. Uses `setMap(map)` to do so.

###show(category)
For loop and if statement to set category's items to show, only if current category. Uses `setMap(map)` to do so.

###hide(category)
For loop and if statement to set category's items to hide, only if current category. Uses `setMap(null)` to do so.

###toggleMarkers(category)
If statement to determine to show all, or show/hide based on the category selected in the user interaction.

###initialize(){
Runs the functions to initialize the map. This must be called somehow to show the map. Runs:
* `setMarkerLocations()`
* `setMapStyles()`
* `markerInitialize()`
