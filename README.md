Hej, I’m Gerd Tunay Schuster, Software Engineer and Aviator

# VFR-Flugplanung & Streckenwetter für Privatpiloten

die App auf __https://app.tunay.io__ unterstützt dich dabei, deine VFR-Flüge übersichtlich und schnell vorzubereiten. Du planst deine Route direkt auf der Karte, ergänzt Flugplätze oder Navigationspunkte und erhältst automatisch wichtige Informationen zu Strecke, Kurs, Flugzeit, Wetter, Wind und Kraftstoffbedarf.

<img width="1566" height="952" alt="Screenshot 2026-10-01 at 14 18 20" src="https://github.com/user-attachments/assets/b66cc58e-35ab-43e7-bbf8-28f20211b380" />

Dabei berücksichtigt die App nicht nur die reine Entfernung zwischen deinen Wegpunkten. Windrichtung und Windgeschwindigkeit fließen ebenfalls in die Berechnung ein, sodass du eine realistischere Einschätzung von Steuerkurs, Groundspeed und voraussichtlicher Flugzeit bekommst.

Für jeden Streckenabschnitt werden aktuelle Wetterinformationen eingebunden. So kannst du Wetter, Wind, Böen, Bewölkung, Temperatur, Luftdruck und Niederschlagswahrscheinlichkeit entlang deiner geplanten Route einfacher überblicken und mögliche problematische Bereiche frühzeitig erkennen.

Auch die Geländeentwicklung entlang der Strecke wird berücksichtigt. Nach der Planung zeigt dir ein Höhenprofil, wie sich das Terrain unter deiner Route verändert. Zusätzlich wird geprüft, ob deine gewählte Flughöhe ausreichend Abstand zum höchsten Gelände bietet.

Mit den hinterlegten Flugzeugdaten kannst du außerdem den voraussichtlichen Kraftstoffbedarf berechnen. Die App zeigt dir unter anderem den benötigten Streckenkraftstoff, Reserven, verbleibenden Kraftstoff und die mögliche Flugdauer. So erkennst du schnell, wenn eine Planung mit den gewählten Einstellungen zu knapp wird.

Auch typische Punkte im Flugprofil wie Top of Climb und Top of Descent können automatisch berechnet und auf der Karte dargestellt werden. Dadurch bekommst du schon vor dem Flug ein besseres Gefühl dafür, wie sich die einzelnen Flugphasen entlang deiner Strecke verteilen.

Deine Route bleibt dabei flexibel: Wegpunkte können jederzeit ergänzt, verschoben oder entfernt werden. Fertige Routen lassen sich exportieren und später wieder importieren.

Die App soll dir damit vor allem eines geben: einen schnellen, visuellen Überblick über deine geplante Strecke und die wichtigsten Einflussfaktoren darauf – Route, Wetter, Wind, Gelände, Zeit und Kraftstoff an einem Ort.

Die Anwendung dient als Unterstützung für Planung und Orientierung. Für die tatsächliche Flugdurchführung müssen weiterhin die offiziellen und für den jeweiligen Flug vorgeschriebenen Informationsquellen verwendet werden.

__https://app.tunay.io__

__https://tunay.io__

> __Warning__ Please be informed that the flight planning with this application is for rough orientation only and may not be used for real flights. Use at your own risk. Please confirm all weather datas at the original source. These are for internal information only and may be wrong, out of date, or incomplete. app.tunay.io assumes no liability for the correctness, accuracy, relevance, reliability or completeness of the information published.

<img width="1062" alt="Screenshot 2023-09-17 at 11 44 48" src="https://github.com/tunayio/tunayio/assets/111220915/ceb0fdb4-b2e9-403c-9df6-17f22e1b937e">
<img width="1237" alt="Screenshot 2023-09-17 at 11 47 41" src="https://github.com/tunayio/tunayio/assets/111220915/042dbab7-be02-4656-9ecf-112732883155">
<img width="749" alt="Screenshot 2023-09-17 at 11 46 02" src="https://github.com/tunayio/tunayio/assets/111220915/f73962b1-50e1-4a53-bd3d-00353e7bd20d">
<img width="961" alt="Screenshot 2023-09-17 at 11 48 44" src="https://github.com/tunayio/tunayio/assets/111220915/55659960-9498-4284-9be0-a0199d745e9a">
<img width="1447" height="784" alt="Screenshot 2026-10-01 at 17 55 26" src="https://github.com/user-attachments/assets/2043b7a9-716b-49b1-bee7-21dfb3bdef0b" />
<img width="1170" height="634" alt="Screenshot 2026-06-07 at 16 00 17" src="https://github.com/user-attachments/assets/2fdce9d2-097f-456d-af0e-d521dd9096f4" />

### free visual VFR route weather for private pilots

The flight-planning module is a client-side route editor and calculation engine built around Mapbox GL, Turf.js, jQuery, Highcharts, and external weather and elevation services. It is intended for rough planning and orientation only; the application explicitly states that it must not be used for real-flight decisions.
A route is stored as an ordered array of longitude/latitude waypoints. Users can add points directly on the map, search for airports and navigation aids, insert a point into an existing leg, drag a waypoint, or remove it. The editor uses screen-space tolerances for waypoint selection, route-segment selection, and snapping to nearby airports or navaids. Each leg is rendered as a great-circle route rather than a simple straight line in map projection, which preserves the correct global route geometry.

The planner maintains its map presentation through GeoJSON sources and Mapbox layers. These layers display the route, waypoint labels, directional arrows, hover previews, airport/navaid candidates, wind information, climb and descent markers, and terrain-related route points. Interactive popups expose leg and waypoint information without leaving the map.

For each leg, the scheduling logic calculates great-circle distance, true course, midpoint position, estimated time en route, cumulative ETA, and total route distance. It fetches current weather for the leg midpoint through an OpenWeather-style “one call” endpoint, including wind, gusts, pressure, temperature, cloud cover, humidity, precipitation probability, and weather description. Wind direction and speed are combined with the configured true airspeed to calculate wind-correction angle, heading, and ground speed. Magnetic variation is obtained through a World Magnetic Model calculation, allowing the planner to derive magnetic heading from true course.

Aircraft settings drive the operational calculations. The setup includes aircraft performance, true airspeed, estimated departure time, fuel burn, available fuel, altitude range, and reserve-related fuel allowances. The module calculates route fuel, reserve fuel, total required fuel, remaining fuel, endurance, and remaining flight time. It highlights negative margins as configuration issues.

When a plan is completed, the module samples terrain elevation along the route and creates an elevation profile with Highcharts. It compares the selected cruise-altitude range with the highest terrain point plus a 2,000 ft AGL safety margin, then reports an issue if the altitude is insufficient. It also estimates and maps top-of-climb and top-of-descent positions; when the route is too short for those phases to be reached, the markers are suppressed and the limitation is reported.

Routes can be exported as a GeoJSON FeatureCollection containing waypoint features and re-imported from GeoJSON. Importing replaces the active route, while the exit flow warns users before discarding an unsaved plan.

### features

- Plan your flight routes with realtime nowcast and forecast (48 hours) global aviation weather along the route.
- Various global meteorological layers like temperature, humidity, dew point, atmospheric pressure and density on MSL, wind and gusts, cloud covering and precipitation.
- Practice in the platform specifically designed for learning the basics of instrument navigation. The RMI (Radio Magnetic Indicator) tool was designed to demonstrate the approximate indication that an RMI would display with varying positions of an aircraft in relation to certain navigational facilities.
- app.tunay.io is a collaborative learning platform that allows pupils to make the learning experience engaging, collaborative, and interactive. a group of pupils joins together at app.tunay.io to improve there skills in radiotelephony and the safety in aviation. once logged into the app, the student can position their virtual aircraft on the map using a compass rose. everyone can see everyone. this method provides additional visual support for any verbal radio course.

