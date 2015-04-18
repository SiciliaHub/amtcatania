# Descrizione
Il 17/04/2015 la municipalizzata del comune di Catania ha pubblicato in formato aperto i dati sul trasporto pubblico: http://www.amt.ct.it/?page_id=4623

# Dati
## Fermate
### File
Il file, scaricato e creato il 18/04/2015, è disponibile [qui](https://github.com/SiciliaHub/amtcatania/blob/master/data/fermate.geojson). Sistema di riferimento lat/lon WGS84 (EPSG:4326).

![2015-04-18_16h48_36](https://cloud.githubusercontent.com/assets/30607/7215902/e9d6aa56-e5ea-11e4-886d-cded315754c1.png)

### Stringa per download dei dati e conversione in GeoJSON
    curl "http://www.amt.ct.it/OpenData/leggifermate.php?linee=101;1-4;144;237;241;244;2-5;429;431N;431R;432;439;443;448;449;4-7;503;522;523;524;534;534;536;538;538;550;555;556;621;621;628N;628R;635;642;701;702;722;726;733;740;801;802;830;830;902;925;927;932;935;ALIBUS;BRT1;D;S2;S2" -s | jq . | in2csv -f json | csvjson --lat Latitudine --lon Longitudine | jq . > fermate.geojson
## Linee
### File
Il file, scaricato e creato il 18/04/2015, è disponibile [qui](https://github.com/SiciliaHub/amtcatania/blob/master/data/linee.geojson). Sistema di riferimento lat/lon WGS84 (EPSG:4326).

![2015-04-18_16h49_21](https://cloud.githubusercontent.com/assets/30607/7215904/fba5af48-e5ea-11e4-95f9-0eda03cef055.png)

### Stringa per download dei dati e conversione in GeoJSON
    curl -s "http://www.amt.ct.it/OpenData/linee.php" | jq "{\"type\": \"FeatureCollection\",  \"features\": [.Lines.Line[] |{\"type\": \"Feature\",\"properties\": {\"name\":.name,\"id\":.id,\"description\":.description,\"timetables\":.timetables,\"routes\":.routes,\"note\":.note[0]},\"geometry\":{\"type\": \"LineString\",\"coordinates\":[.polyline[] | [.[1],.[0]]]}}]}" > linee.geojson
