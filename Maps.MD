# Introduction
Google Maps is an incredible set of APIs available to us to build location based applications. Register for an API key and build your
first Map Application to start learning how to build Maps Apps.

# Example

```html

<html>
<body>
		<input type="button" value="Drop Pin" onclick="dropPin()"> Drop a pin marker on the map <br>

		<div id="map"></div>
		<style>
			#map {
				height: 400px;
			}
		</style>
		<script src="https://maps.googleapis.com/maps/api/js"></script>
		<script>
			var directionsDisplay;
			var map;
			var endMarker;

			function initialize() {
				directionsDisplay = new google.maps.DirectionsRenderer();
				var paris = new google.maps.LatLng(48.86100157399595,2.335891842842086);
				var mapOption = {
					zoom: 7,
					center: paris
				}
				map = new google.maps.Map(document.getElementBy.Id("map"),mapOption);
				directionsDisplay.setMap(map);
			}
			function dropPin() {
				if (endMarker) {
					endMarker.setMap(null);
				}
				endMarker = new google.maps.Marker({
					position: map.getCenter(),
					map: map,
					draggable: true,
				});
				google.maps.event.addListener(endMarker, 'dragend', function() {

				});

			}
			google.maps.event.addDomListener(window, 'load', initialize);
		</script>
</body>
</html>

```

# Learning Outcomes
 * How to use Google Maps APIs inside HTML5 Apps
 * How to build rich Map Apps with Google Maps components
