---
layout: post
title: "Geolocation with the Google Maps API"
date: 2014-07-28 22:16:05 -0400
comments: true
categories: 
---
According to Google, "Geolocation refers to the identification of the geographic location of a user or computing device via a variety of data collection mechanisms."

In simpler terms, geolocation is how Google Maps figures out where you are. In order to incorporate this technology into your app, you need to use the Google Maps Javascript API. The documentation can be found at https://developers.google.com/maps/articles/geolocation (copy and paste into browser). An example of the code can be found at https://developers.google.com/maps/documentation/javascript/examples/map-geolocation (copy and paste into browser). It has also been pasted below. While it may be of interest to some people to go through each line of the code and its function, I think it would probably me more efficient/practical to explain the code with much less resolution.

<!-- more -->

``` html
<!DOCTYPE html>
<html>
  <head>
    <title>Geolocation</title>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no">
    <meta charset="utf-8">
    <style>
      html, body, #map-canvas {
        height: 100%;
        margin: 0px;
        padding: 0px
      }
    </style>
    <script src="https://maps.googleapis.com/maps/api/js?v=3.exp"></script>

    <script>
// Note: This example requires that you consent to location sharing when
// prompted by your browser. If you see a blank space instead of the map, this
// is probably because you have denied permission for location sharing.

var map;

function initialize() {
  var mapOptions = {
    zoom: 6
  };
  map = new google.maps.Map(document.getElementById('map-canvas'),
      mapOptions);

  // Try HTML5 geolocation
  if(navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(function(position) {
      var pos = new google.maps.LatLng(position.coords.latitude,
                                       position.coords.longitude);

      var infowindow = new google.maps.InfoWindow({
        map: map,
        position: pos,
        content: 'Location found using HTML5.'
      });

      map.setCenter(pos);
    }, function() {
      handleNoGeolocation(true);
    });
  } else {
    // Browser doesn't support Geolocation
    handleNoGeolocation(false);
  }
}

function handleNoGeolocation(errorFlag) {
  if (errorFlag) {
    var content = 'Error: The Geolocation service failed.';
  } else {
    var content = 'Error: Your browser doesn\'t support geolocation.';
  }

  var options = {
    map: map,
    position: new google.maps.LatLng(60, 105),
    content: content
  };

  var infowindow = new google.maps.InfoWindow(options);
  map.setCenter(options.position);
}

google.maps.event.addDomListener(window, 'load', initialize);

    </script>
  </head>
  <body>
    <div id="map-canvas"></div>
  </body>
</html>
```

First, it should be noted that it would be much better practice to encapsulate all of this javascript in its own file, let's call it map.js, and reference it in the html file as follows: `<script type="text/javascript" src="map.js"></script>` (even better would be if the map.js were in a javascripts directory as well).

Because of line 27, the element with the id, 'map-canvas', is going to contain the Google Map. Line 31 really just gives the conditional that the browser supports HTML5, in which case, geolocation should be possible. If it doesn't it will default to setting the map to center on Siberia, as indicated in lines 59-66.

The meat of this code base is really in lines 32-34, in which the actual geolocation happens. The navigator.geolocation.getCurrentPosition method gets the geolocated coordinates, and the position variable (which contains data from the geolocation) is passed into an anonymous function. In line 33, a LatLng object is created from the position variable, so the rest of the Google Maps API can use the data, such as in line 42. The LatLng object is passed into the setCenter method to center the map on the geolocated coordinates.

While in retrospect, this code base really wasn't that complex, it certainly intimidated me at first, so I hope my breaking down the important parts of it helped.