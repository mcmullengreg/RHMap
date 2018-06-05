# Google Map for Rose-Hulman

This macro contains the [Google Map API JavaScript v3](https://developers.google.com/maps/faq) to render an interactive campus map for the Rose-Hulman.edu Website.

This documentation consists of resources, data structure and flow, and the defined functions for initializing the map. There are many tools and resources available to continue the customization of this map. Please use the resources below for more details.

## Categories

1. Academic
2. Dining
3. Recreation
4. Housing
5. Support
6. Parking
7. Religion
8. Police
9. Health

## Resources
The following is a list of resources for the API documentation, key and information to login to the API console:

* API Console & Reporting: https://code.google.com/apis/console
* API Documentation: https://developers.google.com/maps/documentation/javascript/tutorial 
* Latitude/Longitude Finder: http://itouchmap.com/latlong.html

## Structure
The data structure follows below:

1. Variable Calls
2. Icon definition
3. Functions:
	* createMarker
	* show
	* hide
	* boxclick
	* showLocation
	* makeSidebar
	* myclick
	* init
	* Parse Data
5. Map Options
6. Build Map and Sidebar

## Variables

* var media = Parameter to select the map data item within Umbraco media picker
* gmarkers[] = array of map markers, assigned a gicon[category], and location via Map Data
* gicons[] = array for marker categories and icon assignment, hard coded icon locations
* openedInfoWindow = sets a blank info window on load, assigned to a clicked map item
* side_bar_html = list rendered to the sidebar on a selected category
* marker = Google Map Marker, shows on category selection
* name, lat, lng, category, html = Pulls data from parsed data of the map data htm file.
* point = uses the lat, lng variables to assign the location
* map = map creation variable

## Functions

The functions defined for this initial phase of the campus map are defined below:

### createMarker(point, name, category, html)
* Creates the marker and stores the data in the marker array.
* Defines the infoWindow on marker selection, and closes it when neccessary.


### show(category)
* Show all markers of a particular category, and ensures the checkbox is checked

### hide(category)
* Hide all markers of a particular category and ensures the checkbox is cleared
* Closes open infoWindow if part of that category

### boxclick(box, category)
* Decides when a checkbox is clicked and calls the show/hide functions as appropriate
* Builds the sidebar list as defined by the category.

### showLocation(name)
* Shows a specific marker, should it be clicked on by the name in the sidebar list

### makeSidebar()
* Builds the sidebar based on the category(-ies) selected by the user, lists all items in said category(-ies)

### myclick(i)
* Picks up the click and opens the info window of the specific item

### init(){
* Definition of which markers should be shown/hidden on load (all are shown by default)

### Parse Data
* Extracts the data from the selected .htm file

`@Model.MediaById(media).Url` is an Umbraco specific way of selecting the .htm file.

## HTML File Updates
To update the html file, download a copy of the most current version. An `<hr />` designates a separation of map items. A pipe (`|`) designates a new item within the map item.

Full structure:
```HTML
Item Name|Longitude|Latitude|Category|
<div class="preview">
	<h2>Item Name</h2>
	<p>Item description</p>
</div>
<hr />
```
