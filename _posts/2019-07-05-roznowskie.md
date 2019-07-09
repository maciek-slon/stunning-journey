---
layout: post
title: Okolice Nowego Sącza
gpx:
 - 2019-07-05.gpx
 - 2019-07-06.gpx
 - 2019-07-07.gpx
 - 2019-07-09.gpx
mapid: 20190705
---

<style>
  #route-info div {
    text-align: center;
  }
</style>

<!--<div id="route-info" style="height: 40px">
  <div id="route-length" style="float: left; width: 25%;">d</div>
  <div id="route-time" style="float: left; width: 25%;">d</div>
  <div id="route-speed" style="float: left; width: 25%;">d</div>
  <div id="route-ascent" style="float: left; width: 25%;">d</div>
</div>-->

<div id="mapid-{{ page.mapid }}" style="width: 100%; height: 400px;"></div>
<script>

  var mymap = L.map('mapid-{{ page.mapid }}', {
    attributionControl: false,
    fullscreenControl: {
        pseudoFullscreen: true // if true, fullscreen to page width and height
    }
  }).setView([51.505, -0.09], 13);

	var OpenTopoMap = L.tileLayer('http://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
		maxZoom: 17,
		attribution: 'Map data: &copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)',
		opacity: 0.5
	});
  
  var Esri_WorldTopoMap = L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}', {
    attribution: 'Tiles &copy; Esri &mdash; Esri, DeLorme, NAVTEQ, TomTom, Intermap, iPC, USGS, FAO, NPS, NRCAN, GeoBase, Kadaster NL, Ordnance Survey, Esri Japan, METI, Esri China (Hong Kong), and the GIS User Community'
  });
  
  var Esri_WorldImagery = L.tileLayer('http://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
    attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
  });
  
  OpenTopoMap.addTo(mymap);
  
{% for gpx in page.gpx %}
  
  var gpx = '{{ site.baseurl }}/public/gpx/{{ gpx }}'; 
  var g = new L.GPX(gpx, {
    async: true,
    marker_options: {
      startIconUrl: '',//'{{ site.baseurl }}/public/images/pin-icon-start.png',
      endIconUrl: '',//'{{ site.baseurl }}/public/images/pin-icon-end.png',
      shadowUrl: ''//'{{ site.baseurl }}/public/images/pin-shadow.png'
    },
    polyline_options: {
      color: "#ff0000",
      opacity: 0.5
    }
  });
  
  g.on('loaded', function(e) {
    mymap.fitBounds(e.target.getBounds());
   
    /*document.getElementById("route-length").innerHTML = (Number(g.get_distance()) / 1000).toFixed(2) + "km";
    
    
    var date = new Date(null);
    date.setSeconds(g.get_moving_time() / 1000); 
    var mov_tm = date.toISOString().substr(11, 8);
    document.getElementById("route-time").innerHTML = mov_tm;
    
    document.getElementById("route-speed").innerHTML = g.get_moving_speed().toFixed(2) + "km/h";
    document.getElementById("route-ascent").innerHTML = g.get_elevation_gain().toFixed(0) + "m";
    
    var dateString = g.get_start_time().format("mmm d, yyyy - H:MM");
    //document.getElementById("route-speed").innerHTML = dateString;*/
  });
  
  g.addTo(mymap);
{% endfor %}  

</script>
