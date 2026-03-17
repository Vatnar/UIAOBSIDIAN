1. The "Community Hazard" Reporter (Crowdsourced Safety)
An app where users pin local hazards (broken streetlights, potholes, icy sidewalks) with photos and severity levels.

Why it hits the A-grade:

Third-party integration: Uses Google Maps API (complex UI).

Advanced UI: Requires handling a map with custom clusters and image uploads.

Push Notifications: Alerts users when a hazard is reported nearby (Firebase Cloud Messaging).

Offline/Online: Needs to cache map data or queue reports if the user has no signal while outside.

Legal/Privacy: Perfect for discussing GDPR and "Public interest" data in your report.


2.
"Silent Guardian"
Bruke Geofencing API til å tracke lokasjoner til telefonen, blir koblet opp mot et globalt kart hvor ulike silent zones er definert. For eksempel et bibliotek etc. Appen vil jobbe med Foreground services eller WorkManager 