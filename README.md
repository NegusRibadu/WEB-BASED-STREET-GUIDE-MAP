<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="initial-scale=1,user-scalable=no,maximum-scale=1,width=device-width">
        <meta name="mobile-web-app-capable" content="yes">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <link rel="stylesheet" href="css/leaflet.css"><link rel="stylesheet" href="css/L.Control.Locate.min.css">
        <link rel="stylesheet" href="css/qgis2web.css"><link rel="stylesheet" href="css/fontawesome-all.min.css">
        <link rel="stylesheet" href="css/leaflet-search.css">
        <link rel="stylesheet" href="css/leaflet-measure.css">
        <style>
        html, body, #map {
            width: 100%;
            height: 100%;
            padding: 0;
            margin: 0;
        }
        </style>
        <title></title>
    </head>
    <body>
        <div id="map">
        </div>
        <script src="js/qgis2web_expressions.js"></script>
        <script src="js/leaflet.js"></script><script src="js/L.Control.Locate.min.js"></script>
        <script src="js/multi-style-layer.js"></script>
        <script src="js/leaflet.rotatedMarker.js"></script>
        <script src="js/leaflet.pattern.js"></script>
        <script src="js/leaflet-hash.js"></script>
        <script src="js/Autolinker.min.js"></script>
        <script src="js/rbush.min.js"></script>
        <script src="js/labelgun.min.js"></script>
        <script src="js/labels.js"></script>
        <script src="js/leaflet-measure.js"></script>
        <script src="js/proj4.js"></script>
        <script src="js/proj4leaflet.js"></script>
        <script src="js/leaflet-search.js"></script>
        <script src="data/roundabout_0.js"></script>
        <script src="data/MajorRoad_1.js"></script>
        <script src="data/MinorRoad_2.js"></script>
        <script src="data/Street_3.js"></script>
        <script src="data/AcademicStructures_4.js"></script>
        <script src="data/Healthfacilities_5.js"></script>
        <script src="data/Church_6.js"></script>
        <script src="data/Mosque_7.js"></script>
        <script src="data/Gasstation_8.js"></script>
        <script src="data/Hotel_9.js"></script>
        <script src="data/Prominentstructure_10.js"></script>
        <script src="data/RecreationalFacility_11.js"></script>
        <script src="data/Significantstrctures_12.js"></script>
        <script>
        var highlightLayer;
        function highlightFeature(e) {
            highlightLayer = e.target;

            if (e.target.feature.geometry.type === 'LineString') {
              highlightLayer.setStyle({
                color: '#ffff00',
              });
            } else {
              highlightLayer.setStyle({
                fillColor: '#ffff00',
                fillOpacity: 1
              });
            }
            highlightLayer.openPopup();
        }
        var crs = new L.Proj.CRS('EPSG:3857', '+proj=merc +a=6378137 +b=6378137 +lat_ts=0 +lon_0=0 +x_0=0 +y_0=0 +k=1 +units=m +nadgrids=@null +wktext +no_defs', {
            resolutions: [2800, 1400, 700, 350, 175, 84, 42, 21, 11.2, 5.6, 2.8, 1.4, 0.7, 0.35, 0.14, 0.07],
        });
        var map = L.map('map', {
            crs: crs,
            continuousWorld: false,
            worldCopyJump: false, 
            zoomControl:true, maxZoom:28, minZoom:1
        }).fitBounds([[9.19379450618772,12.463916355951245],[9.215855592324601,12.506981481525743]]);
        var hash = new L.Hash(map);
        map.attributionControl.setPrefix('<a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');
        var autolinker = new Autolinker({truncate: {length: 30, location: 'smart'}});
        L.control.locate({locateOptions: {maxZoom: 19}}).addTo(map);
        var measureControl = new L.Control.Measure({
            position: 'topleft',
            primaryLengthUnit: 'meters',
            secondaryLengthUnit: 'kilometers',
            primaryAreaUnit: 'sqmeters',
            secondaryAreaUnit: 'hectares'
        });
        measureControl.addTo(map);
        document.getElementsByClassName('leaflet-control-measure-toggle')[0]
        .innerHTML = '';
        document.getElementsByClassName('leaflet-control-measure-toggle')[0]
        .className += ' fas fa-ruler';
        var bounds_group = new L.featureGroup([]);
        function setBounds() {
        }
        function pop_roundabout_0(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ogc_fid'] !== null ? autolinker.link(feature.properties['ogc_fid'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(feature.properties['id'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <th scope="row">name</th>\
                        <td>' + (feature.properties['name'] !== null ? autolinker.link(feature.properties['name'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_roundabout_0_0() {
            return {
                pane: 'pane_roundabout_0',
                opacity: 1,
                color: 'rgba(224,238,228,1.0)',
                dashArray: '',
                lineCap: 'butt',
                lineJoin: 'miter',
                weight: 2.0, 
                fill: true,
                fillOpacity: 1,
                fillColor: 'rgba(39,39,39,1.0)',
                interactive: true,
            }
        }
        map.createPane('pane_roundabout_0');
        map.getPane('pane_roundabout_0').style.zIndex = 400;
        map.getPane('pane_roundabout_0').style['mix-blend-mode'] = 'normal';
        var layer_roundabout_0 = new L.geoJson(json_roundabout_0, {
            attribution: '',
            interactive: true,
            dataVar: 'json_roundabout_0',
            layerName: 'layer_roundabout_0',
            pane: 'pane_roundabout_0',
            onEachFeature: pop_roundabout_0,
            style: style_roundabout_0_0,
        });
        bounds_group.addLayer(layer_roundabout_0);
        map.addLayer(layer_roundabout_0);
        function pop_MajorRoad_1(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ogc_fid'] !== null ? autolinker.link(feature.properties['ogc_fid'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['pkuid'] !== null ? autolinker.link(feature.properties['pkuid'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <th scope="row">name</th>\
                        <td>' + (feature.properties['name'] !== null ? autolinker.link(feature.properties['name'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_MajorRoad_1_0() {
            return {
                pane: 'pane_MajorRoad_1',
                opacity: 1,
                color: 'rgba(0,0,0,1.0)',
                dashArray: '',
                lineCap: 'round',
                lineJoin: 'round',
                weight: 6.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        function style_MajorRoad_1_1() {
            return {
                pane: 'pane_MajorRoad_1',
                opacity: 1,
                color: 'rgba(194,188,0,1.0)',
                dashArray: '',
                lineCap: 'round',
                lineJoin: 'round',
                weight: 4.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane_MajorRoad_1');
        map.getPane('pane_MajorRoad_1').style.zIndex = 401;
        map.getPane('pane_MajorRoad_1').style['mix-blend-mode'] = 'normal';
        var layer_MajorRoad_1 = new L.geoJson.multiStyle(json_MajorRoad_1, {
            attribution: '',
            interactive: true,
            dataVar: 'json_MajorRoad_1',
            layerName: 'layer_MajorRoad_1',
            pane: 'pane_MajorRoad_1',
            onEachFeature: pop_MajorRoad_1,
            styles: [style_MajorRoad_1_0,style_MajorRoad_1_1,]
        });
        bounds_group.addLayer(layer_MajorRoad_1);
        map.addLayer(layer_MajorRoad_1);
        function pop_MinorRoad_2(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['fid'] !== null ? autolinker.link(feature.properties['fid'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <th scope="row">Name</th>\
                        <td>' + (feature.properties['Name'] !== null ? autolinker.link(feature.properties['Name'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_MinorRoad_2_0() {
            return {
                pane: 'pane_MinorRoad_2',
                opacity: 1,
                color: 'rgba(224,238,228,1.0)',
                dashArray: '',
                lineCap: 'round',
                lineJoin: 'round',
                weight: 7.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        function style_MinorRoad_2_1() {
            return {
                pane: 'pane_MinorRoad_2',
                opacity: 1,
                color: 'rgba(53,53,53,1.0)',
                dashArray: '',
                lineCap: 'round',
                lineJoin: 'round',
                weight: 3.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane_MinorRoad_2');
        map.getPane('pane_MinorRoad_2').style.zIndex = 402;
        map.getPane('pane_MinorRoad_2').style['mix-blend-mode'] = 'normal';
        var layer_MinorRoad_2 = new L.geoJson.multiStyle(json_MinorRoad_2, {
            attribution: '',
            interactive: true,
            dataVar: 'json_MinorRoad_2',
            layerName: 'layer_MinorRoad_2',
            pane: 'pane_MinorRoad_2',
            onEachFeature: pop_MinorRoad_2,
            styles: [style_MinorRoad_2_0,style_MinorRoad_2_1,]
        });
        bounds_group.addLayer(layer_MinorRoad_2);
        map.addLayer(layer_MinorRoad_2);
        function pop_Street_3(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ogc_fid'] !== null ? autolinker.link(feature.properties['ogc_fid'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(feature.properties['id'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <th scope="row">name</th>\
                        <td>' + (feature.properties['name'] !== null ? autolinker.link(feature.properties['name'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Street_3_0() {
            return {
                pane: 'pane_Street_3',
                opacity: 1,
                color: 'rgba(224,238,228,1.0)',
                dashArray: '',
                lineCap: 'round',
                lineJoin: 'round',
                weight: 4.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        function style_Street_3_1() {
            return {
                pane: 'pane_Street_3',
                opacity: 1,
                color: 'rgba(106,106,106,1.0)',
                dashArray: '',
                lineCap: 'round',
                lineJoin: 'round',
                weight: 1.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane_Street_3');
        map.getPane('pane_Street_3').style.zIndex = 403;
        map.getPane('pane_Street_3').style['mix-blend-mode'] = 'normal';
        var layer_Street_3 = new L.geoJson.multiStyle(json_Street_3, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Street_3',
            layerName: 'layer_Street_3',
            pane: 'pane_Street_3',
            onEachFeature: pop_Street_3,
            styles: [style_Street_3_0,style_Street_3_1,]
        });
        bounds_group.addLayer(layer_Street_3);
        map.addLayer(layer_Street_3);
        function pop_AcademicStructures_4(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_AcademicStructures_4_0() {
            return {
                pane: 'pane_AcademicStructures_4',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/education_university.svg',
            iconSize: [15.2, 15.2]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_AcademicStructures_4');
        map.getPane('pane_AcademicStructures_4').style.zIndex = 404;
        map.getPane('pane_AcademicStructures_4').style['mix-blend-mode'] = 'normal';
        var layer_AcademicStructures_4 = new L.geoJson(json_AcademicStructures_4, {
            attribution: '',
            interactive: true,
            dataVar: 'json_AcademicStructures_4',
            layerName: 'layer_AcademicStructures_4',
            pane: 'pane_AcademicStructures_4',
            onEachFeature: pop_AcademicStructures_4,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_AcademicStructures_4_0(feature));
            },
        });
        bounds_group.addLayer(layer_AcademicStructures_4);
        map.addLayer(layer_AcademicStructures_4);
        function pop_Healthfacilities_5(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTINGS'] !== null ? autolinker.link(feature.properties['EASTINGS'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHINGS'] !== null ? autolinker.link(feature.properties['NORTHINGS'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Healthfacilities_5_0() {
            return {
                pane: 'pane_Healthfacilities_5',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/health_doctors.svg',
            iconSize: [15.2, 15.2]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_Healthfacilities_5');
        map.getPane('pane_Healthfacilities_5').style.zIndex = 405;
        map.getPane('pane_Healthfacilities_5').style['mix-blend-mode'] = 'normal';
        var layer_Healthfacilities_5 = new L.geoJson(json_Healthfacilities_5, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Healthfacilities_5',
            layerName: 'layer_Healthfacilities_5',
            pane: 'pane_Healthfacilities_5',
            onEachFeature: pop_Healthfacilities_5,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_Healthfacilities_5_0(feature));
            },
        });
        bounds_group.addLayer(layer_Healthfacilities_5);
        map.addLayer(layer_Healthfacilities_5);
        function pop_Church_6(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Church_6_0() {
            return {
                pane: 'pane_Church_6',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/religion=christian.svg',
            iconSize: [14.44, 14.44]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_Church_6');
        map.getPane('pane_Church_6').style.zIndex = 406;
        map.getPane('pane_Church_6').style['mix-blend-mode'] = 'normal';
        var layer_Church_6 = new L.geoJson(json_Church_6, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Church_6',
            layerName: 'layer_Church_6',
            pane: 'pane_Church_6',
            onEachFeature: pop_Church_6,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_Church_6_0(feature));
            },
        });
        bounds_group.addLayer(layer_Church_6);
        map.addLayer(layer_Church_6);
        function pop_Mosque_7(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Mosque_7_0() {
            return {
                pane: 'pane_Mosque_7',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/place_of_worship_islamic3.svg',
            iconSize: [12.92, 12.92]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_Mosque_7');
        map.getPane('pane_Mosque_7').style.zIndex = 407;
        map.getPane('pane_Mosque_7').style['mix-blend-mode'] = 'normal';
        var layer_Mosque_7 = new L.geoJson(json_Mosque_7, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Mosque_7',
            layerName: 'layer_Mosque_7',
            pane: 'pane_Mosque_7',
            onEachFeature: pop_Mosque_7,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_Mosque_7_0(feature));
            },
        });
        bounds_group.addLayer(layer_Mosque_7);
        map.addLayer(layer_Mosque_7);
        function pop_Gasstation_8(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Gasstation_8_0() {
            return {
                pane: 'pane_Gasstation_8',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/gas.svg',
            iconSize: [15.2, 15.2]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_Gasstation_8');
        map.getPane('pane_Gasstation_8').style.zIndex = 408;
        map.getPane('pane_Gasstation_8').style['mix-blend-mode'] = 'normal';
        var layer_Gasstation_8 = new L.geoJson(json_Gasstation_8, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Gasstation_8',
            layerName: 'layer_Gasstation_8',
            pane: 'pane_Gasstation_8',
            onEachFeature: pop_Gasstation_8,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_Gasstation_8_0(feature));
            },
        });
        bounds_group.addLayer(layer_Gasstation_8);
        map.addLayer(layer_Gasstation_8);
        function pop_Hotel_9(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Hotel_9_0() {
            return {
                pane: 'pane_Hotel_9',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/accommodation_hotel.svg',
            iconSize: [11.399999999999999, 11.399999999999999]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_Hotel_9');
        map.getPane('pane_Hotel_9').style.zIndex = 409;
        map.getPane('pane_Hotel_9').style['mix-blend-mode'] = 'normal';
        var layer_Hotel_9 = new L.geoJson(json_Hotel_9, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Hotel_9',
            layerName: 'layer_Hotel_9',
            pane: 'pane_Hotel_9',
            onEachFeature: pop_Hotel_9,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_Hotel_9_0(feature));
            },
        });
        bounds_group.addLayer(layer_Hotel_9);
        map.addLayer(layer_Hotel_9);
        function pop_Prominentstructure_10(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Prominentstructure_10_0() {
            return {
                pane: 'pane_Prominentstructure_10',
        rotationAngle: 0.0,
        rotationOrigin: 'center center',
        icon: L.icon({
            iconUrl: 'markers/tourism=museum.svg',
            iconSize: [11.399999999999999, 11.399999999999999]
        }),
                interactive: true,
            }
        }
        map.createPane('pane_Prominentstructure_10');
        map.getPane('pane_Prominentstructure_10').style.zIndex = 410;
        map.getPane('pane_Prominentstructure_10').style['mix-blend-mode'] = 'normal';
        var layer_Prominentstructure_10 = new L.geoJson(json_Prominentstructure_10, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Prominentstructure_10',
            layerName: 'layer_Prominentstructure_10',
            pane: 'pane_Prominentstructure_10',
            onEachFeature: pop_Prominentstructure_10,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style_Prominentstructure_10_0(feature));
            },
        });
        bounds_group.addLayer(layer_Prominentstructure_10);
        map.addLayer(layer_Prominentstructure_10);
        function pop_RecreationalFacility_11(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTING'] !== null ? autolinker.link(feature.properties['EASTING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHING'] !== null ? autolinker.link(feature.properties['NORTHING'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_RecreationalFacility_11_0() {
            return {
                pane: 'pane_RecreationalFacility_11',
                radius: 4.0,
                opacity: 1,
                color: 'rgba(50,87,128,1.0)',
                dashArray: '',
                lineCap: 'butt',
                lineJoin: 'miter',
                weight: 2.0,
                fill: true,
                fillOpacity: 1,
                fillColor: 'rgba(103,148,200,1.0)',
                interactive: true,
            }
        }
        map.createPane('pane_RecreationalFacility_11');
        map.getPane('pane_RecreationalFacility_11').style.zIndex = 411;
        map.getPane('pane_RecreationalFacility_11').style['mix-blend-mode'] = 'normal';
        var layer_RecreationalFacility_11 = new L.geoJson(json_RecreationalFacility_11, {
            attribution: '',
            interactive: true,
            dataVar: 'json_RecreationalFacility_11',
            layerName: 'layer_RecreationalFacility_11',
            pane: 'pane_RecreationalFacility_11',
            onEachFeature: pop_RecreationalFacility_11,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.circleMarker(latlng, style_RecreationalFacility_11_0(feature));
            },
        });
        bounds_group.addLayer(layer_RecreationalFacility_11);
        map.addLayer(layer_RecreationalFacility_11);
        function pop_Significantstrctures_12(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (i in e.target._eventParents) {
                        e.target._eventParents[i].resetStyle(e.target);
                    }
                    if (typeof layer.closePopup == 'function') {
                        layer.closePopup();
                    } else {
                        layer.eachLayer(function(feature){
                            feature.closePopup()
                        });
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2"><strong>NAME</strong><br />' + (feature.properties['NAME'] !== null ? autolinker.link(feature.properties['NAME'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['EASTINGS'] !== null ? autolinker.link(feature.properties['EASTINGS'].toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NORTHINGS'] !== null ? autolinker.link(feature.properties['NORTHINGS'].toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            layer.bindPopup(popupContent, {maxHeight: 400});
        }

        function style_Significantstrctures_12_0() {
            return {
                pane: 'pane_Significantstrctures_12',
                radius: 5.0,
                opacity: 1,
                color: 'rgba(255,255,255,1.0)',
                dashArray: '',
                lineCap: 'butt',
                lineJoin: 'miter',
                weight: 2.0,
                fill: true,
                fillOpacity: 1,
                fillColor: 'rgba(0,0,0,0.6666666666666666)',
                interactive: true,
            }
        }
        map.createPane('pane_Significantstrctures_12');
        map.getPane('pane_Significantstrctures_12').style.zIndex = 412;
        map.getPane('pane_Significantstrctures_12').style['mix-blend-mode'] = 'normal';
        var layer_Significantstrctures_12 = new L.geoJson(json_Significantstrctures_12, {
            attribution: '',
            interactive: true,
            dataVar: 'json_Significantstrctures_12',
            layerName: 'layer_Significantstrctures_12',
            pane: 'pane_Significantstrctures_12',
            onEachFeature: pop_Significantstrctures_12,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.circleMarker(latlng, style_Significantstrctures_12_0(feature));
            },
        });
        bounds_group.addLayer(layer_Significantstrctures_12);
        map.addLayer(layer_Significantstrctures_12);
        var baseMaps = {};
        L.control.layers(baseMaps,{'<img src="legend/Significantstrctures_12.png" /> Significant strctures': layer_Significantstrctures_12,'<img src="legend/RecreationalFacility_11.png" /> Recreational Facility': layer_RecreationalFacility_11,'<img src="legend/Prominentstructure_10.png" /> Prominent structure': layer_Prominentstructure_10,'<img src="legend/Hotel_9.png" /> Hotel': layer_Hotel_9,'<img src="legend/Gasstation_8.png" /> Gas station': layer_Gasstation_8,'<img src="legend/Mosque_7.png" /> Mosque': layer_Mosque_7,'<img src="legend/Church_6.png" /> Church': layer_Church_6,'<img src="legend/Healthfacilities_5.png" /> Health facilities': layer_Healthfacilities_5,'<img src="legend/AcademicStructures_4.png" /> Academic Structures': layer_AcademicStructures_4,'<img src="legend/Street_3.png" /> Street': layer_Street_3,'<img src="legend/MinorRoad_2.png" /> Minor Road': layer_MinorRoad_2,'<img src="legend/MajorRoad_1.png" /> Major Road': layer_MajorRoad_1,'<img src="legend/roundabout_0.png" /> roundabout': layer_roundabout_0,},{collapsed:false}).addTo(map);
        setBounds();
        var i = 0;
        layer_MajorRoad_1.eachLayer(function(layer) {
            var context = {
                feature: layer.feature,
                variables: {}
            };
            layer.bindTooltip((layer.feature.properties['name'] !== null?String('<div style="color: #000000; font-size: 12pt; font-family: \'MS Shell Dlg 2\', sans-serif;">' + layer.feature.properties['name']) + '</div>':''), {permanent: true, offset: [-0, -16], className: 'css_MajorRoad_1'});
            labels.push(layer);
            totalMarkers += 1;
              layer.added = true;
              addLabel(layer, i);
              i++;
        });
        var i = 0;
        layer_MinorRoad_2.eachLayer(function(layer) {
            var context = {
                feature: layer.feature,
                variables: {}
            };
            layer.bindTooltip((layer.feature.properties['Name'] !== null?String('<div style="color: #000000; font-size: 7pt; font-family: \'MS Shell Dlg 2\', sans-serif;">' + layer.feature.properties['Name']) + '</div>':''), {permanent: true, offset: [-0, -16], className: 'css_MinorRoad_2'});
            labels.push(layer);
            totalMarkers += 1;
              layer.added = true;
              addLabel(layer, i);
              i++;
        });
        var i = 0;
        layer_Street_3.eachLayer(function(layer) {
            var context = {
                feature: layer.feature,
                variables: {}
            };
            layer.bindTooltip((layer.feature.properties['name'] !== null?String('<div style="color: #000000; font-size: 7pt; font-family: \'MS Shell Dlg 2\', sans-serif;">' + layer.feature.properties['name']) + '</div>':''), {permanent: true, offset: [-0, -16], className: 'css_Street_3'});
            labels.push(layer);
            totalMarkers += 1;
              layer.added = true;
              addLabel(layer, i);
              i++;
        });
        map.addControl(new L.Control.Search({
            layer: layer_Street_3,
            initial: false,
            hideMarkerOnCollapse: true,
            propertyName: 'name'}));
        document.getElementsByClassName('search-button')[0].className +=
         ' fa fa-binoculars';
        resetLabels([layer_MajorRoad_1,layer_MinorRoad_2,layer_Street_3,layer_AcademicStructures_4,layer_Healthfacilities_5,layer_Church_6,layer_Mosque_7,layer_Gasstation_8,layer_Hotel_9,layer_Prominentstructure_10,layer_RecreationalFacility_11,layer_Significantstrctures_12]);
        map.on("zoomend", function(){
            resetLabels([layer_MajorRoad_1,layer_MinorRoad_2,layer_Street_3,layer_AcademicStructures_4,layer_Healthfacilities_5,layer_Church_6,layer_Mosque_7,layer_Gasstation_8,layer_Hotel_9,layer_Prominentstructure_10,layer_RecreationalFacility_11,layer_Significantstrctures_12]);
        });
        map.on("layeradd", function(){
            resetLabels([layer_MajorRoad_1,layer_MinorRoad_2,layer_Street_3,layer_AcademicStructures_4,layer_Healthfacilities_5,layer_Church_6,layer_Mosque_7,layer_Gasstation_8,layer_Hotel_9,layer_Prominentstructure_10,layer_RecreationalFacility_11,layer_Significantstrctures_12]);
        });
        map.on("layerremove", function(){
            resetLabels([layer_MajorRoad_1,layer_MinorRoad_2,layer_Street_3,layer_AcademicStructures_4,layer_Healthfacilities_5,layer_Church_6,layer_Mosque_7,layer_Gasstation_8,layer_Hotel_9,layer_Prominentstructure_10,layer_RecreationalFacility_11,layer_Significantstrctures_12]);
        });
        </script>
    </body>
</html>
