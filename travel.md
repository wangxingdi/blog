---
title: "Travel Map"
date: 2019-08-30
type: "page"
url: /travel
draft: false
---

<!-- <a id="travelbook" href="/categories/travel/">我的足迹</a> ->

<!-- HTML -->
<div id="travelmap"></div>

<!-- Styles -->
<style>
#travelbook {
  float: right;
  font-weight: 900;
}
#travelmap {
  width: 100%;
  height: 500px;
}
.amcharts-chart-div a {
  display: none !important;
}
</style>

<!-- Resources -->
<script src="https://www.amcharts.com/lib/3/ammap.js"></script>
<script src="https://www.amcharts.com/lib/3/maps/js/worldLow.js"></script>
<script src="https://www.amcharts.com/lib/3/maps/js/worldHigh.js"></script>
<script src="https://www.amcharts.com/lib/3/themes/light.js"></script>

<!-- Chart code -->
<script>
/**
 * Define SVG path for target icon
 */
var targetSVG = "M9,0C4.029,0,0,4.029,0,9s4.029,9,9,9s9-4.029,9-9S13.971,0,9,0z M9,15.93 c-3.83,0-6.93-3.1-6.93-6.93S5.17,2.07,9,2.07s6.93,3.1,6.93,6.93S12.83,15.93,9,15.93 M12.5,9c0,1.933-1.567,3.5-3.5,3.5S5.5,10.933,5.5,9S7.067,5.5,9,5.5 S12.5,7.067,12.5,9z";

/**
 * Create the cities
 * https://www.latlong.net
 */
const cities = [
  {
    "title": "Phuket",
    "latitude": 7.979026,
    "longitude": 98.335533,
  },
  {
    "title": "Beijing",
    "latitude": 39.904202,
    "longitude": 116.407394,
  },
  {
    "title": "Xi'an",
    "latitude": 34.269420,
    "longitude": 108.906170,
  },
  {
    "title": "Mukden",
    "latitude": 41.802160,
    "longitude": 123.383060,
  },
  {
    "title": "Changchun",
    "latitude": 43.866950,
    "longitude": 125.338040,
  },
  {
    "title": "Harbin",
    "latitude": 45.751930,
    "longitude": 126.648040,
  },
  
];
for (var i = 0; i < cities.length; ++i){
  cities[i]["zoomLevel"] = 5;
  cities[i]["scale"] = 0.5;
  cities[i]["svgPath"] = targetSVG;
  cities[i]["scale"] = 0.5;
}

/**
 * Create the map
 */
var map = AmCharts.makeChart( "travelmap", {
  "type": "map",
  "projection": "mercator",
  "theme": "light",
  "imagesSettings": {
    "rollOverColor": "#089282",
    "rollOverScale": 3,
    "selectedScale": 3,
    "selectedColor": "#089282",
    "color": "#13564e",
  },
  "areasSettings": {
    autoZoom: true,
    "unlistedAreasColor": "#15A892",
    "outlineThickness": 1,
    "color": "#B4B4B7",
    "colorSolid": "#84ADE9",
    "selectedColor": "#84ADE9",
    "outlineColor": "#666666",
    "rollOverColor": "#9EC2F7",
    "rollOverOutlineColor": "#000000"
  },
  "dataProvider": {
    "map": "worldHigh",
    getAreasFromMap: true,
    "images": cities,
    areas: [{
                "id": "CN",
                "showAsSelected": true
            },
			{
                "id": "TH",
                "showAsSelected": true
            },
        ],
  },
  "export": {
    "enabled": false,
  },
} );

</script>