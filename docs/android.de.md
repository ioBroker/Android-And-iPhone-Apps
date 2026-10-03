<img src="images/app-icon.png" width="88" align="right" alt="ioBroker Visu App-Icon" />

# ioBroker Visu — Android

[⬅️ Zurück zur Übersicht](../README.de.md) · 🇬🇧 [English version](android.md)

**📲 [Bei Google Play installieren](https://play.google.com/store/apps/details?id=com.iobroker.visu)**

| | |
|---|---|
| **App-Name** | ioBroker Visu |
| **Paket** | `com.iobroker.visu` |
| **Herausgeber** | ioBroker GmbH |
| **Preis** | Kostenlos — keine Werbung, keine In-App-Käufe |
| **Kategorie** | Lifestyle |
| **Mindestens Android** | 8.0 (API 26) |
| **Sprachen** | Englisch, Deutsch, Russisch |
| **Store-Link** | <https://play.google.com/store/apps/details?id=com.iobroker.visu> |

> Die Vorgänger-App `net.iobroker.vis` wird nicht mehr weiterentwickelt. Bitte
> **ioBroker Visu** (`com.iobroker.visu`) installieren.

---

## Screenshots

| Deine Visualisierung | Verbindungseinstellungen | Darstellung |
|---|---|---|
| <img src="images/android/vis-dashboard-phone.png" width="230" alt="vis-Dashboard auf einem Android-Smartphone" /> | <img src="images/android/settings-connection-phone.png" width="230" alt="Verbindungseinstellungen" /> | <img src="images/android/settings-appearance-phone.png" width="230" alt="Darstellungseinstellungen" /> |

Auf Tablets nutzen dieselben Ansichten die volle Breite:

| Dashboard (quer) | Navigationsmenü |
|---|---|
| <img src="images/android/vis-dashboard-tablet-landscape.png" width="420" alt="Dashboard auf einem Tablet im Querformat" /> | <img src="images/android/vis-menu-tablet-landscape.png" width="420" alt="Navigationsmenü auf einem Tablet" /> |

| Dashboard (hoch) | Navigationsmenü (hoch) | Vollständige Einstellungsliste |
|---|---|---|
| <img src="images/android/vis-dashboard-tablet-portrait.png" width="260" alt="Dashboard auf einem Tablet im Hochformat" /> | <img src="images/android/vis-menu-tablet-portrait.png" width="260" alt="Navigationsmenü auf einem Tablet im Hochformat" /> | <img src="images/android/settings-full-tablet.png" width="320" alt="Vollständige Einstellungsliste" /> |

*Das sind die aktuellen Google-Play-Screenshots. Die App wird laufend weiterentwickelt, der
Einstellungsbildschirm der neuesten Version kann daher anders gegliedert sein als hier zu
sehen — die Referenz unten beschreibt die aktuelle Struktur.*

---

## Funktionsumfang

Die App zeigt die Visualisierung, die ohnehin schon auf deiner ioBroker-Installation läuft, in
einer darauf abgestimmten Vollbild-WebView und ergänzt alles, was ein Browser nicht kann: eine
gespeicherte Verbindung, automatisches Umschalten zwischen lokal und extern,
Homescreen-Widgets, Push-Benachrichtigungen, Gerätesensoren, Matter-Inbetriebnahme und
Kiosk-Verhalten.

### Unterstützte Visualisierungen

`vis-2` · `vis` · `lovelace` · `material` · `jarvis` · `iQontrol` · `habpanel` · `devices`

Die Auswahl bestimmt lediglich, welche URL die App öffnet — alles andere, was deine
web-Instanz ausliefert, lässt sich ebenfalls verwenden. Standardport ist **8082**, außer bei
`lovelace`: dort **8091**.

### Verbindung

- **Lokal** — IP und Port der web-Instanz, z. B. `192.168.1.10:8082`. Ein reines `IP:PORT`
  wird automatisch vervollständigt, `https://` kann explizit angegeben werden. Benutzername
  und Passwort führen optional einen automatischen Login durch.
- **Pro-Cloud** — dein [ioBroker.pro](https://iobroker.pro)-Konto für den Zugriff von außen.
  Das Abonnement wird gegen die Cloud geprüft; auf Wunsch zeigt ein Pro-Logo in der Ecke an,
  dass gerade die Cloud-Verbindung genutzt wird.
- **Eigene Cloud** — statt ioBroker.pro eine beliebige selbst betriebene URL.
- **WLAN-SSIDs** — kommagetrennte Liste deiner Heimnetze. Solange eines davon verbunden ist,
  nutzt die App die lokale URL, sonst die Cloud.
- **VPN-Erkennung** — ist ein VPN aktiv, kann die App die lokale URL vorschlagen oder still
  verwenden, weil die lokale Adresse durch den Tunnel wieder erreichbar ist.
- **QR-Code-Einrichtung** — im Tab *Lokal* liest ein Scanner den von ioBroker erzeugten
  `iotConfig`-Code und füllt Port, IP, Cloud-Benutzer und Passwort in einem Schritt aus.
- **Selbstsignierte Zertifikate** — je Projekt für lokale HTTPS-Instanzen erlaubbar.
- **Sitzungswiederherstellung** — eine abgelaufene Sitzung erzeugt keinen Fehler, sondern nur
  eine Weiterleitung auf eine Login-Seite. Die App erneuert das Sitzungs-Cookie vor Ablauf,
  erneuert es erneut beim Zurückkehren in den Vordergrund und erkennt eine Login-Seite an
  ihrer URL, meldet sich still neu an und kehrt zur vorherigen Seite zurück.

### Homescreen-Widgets

Zwei Kacheltypen — ein **Toggle**, der einen Datenpunkt schaltet, und eine **Analog**-Kachel,
die einen Zahlenwert anzeigt. Beide funktionieren, ohne die App zu öffnen, lesen und schreiben
zuerst lokal mit Cloud-Fallback und werden per Push aktualisiert.

➡️ **[widgets.de.md](widgets.de.md) — wie Widgets aktualisiert werden und was dafür
einzurichten ist.**

### Push-Benachrichtigungen

Aus ioBroker gesendete Nachrichten (`iot.0.app.message`, optional mit `app.title`,
`app.expire` und `app.priority`) kommen als Android-Benachrichtigung mit bis zu drei
Aktionsknöpfen an; die gedrückte Aktion wird nach ioBroker zurückgeschrieben. Eine
Benachrichtigung kann gezielt bestimmte Geräte ansprechen und eine zu öffnende URL
mitführen. Push setzt ein gültiges ioBroker.pro-Konto voraus: Das Gerät abonniert ein aus
deinem Pro-Benutzernamen abgeleitetes Thema.

### Gerätedaten (Telemetrie)

Die App kann nach ioBroker zurückmelden: **Akkustand** und Ladezustand,
**Bildschirmhelligkeit** (in beide Richtungen — ein Schreiben auf den Datenpunkt dimmt das
Gerät), **Standort**, **WLAN-SSID**, **Verbindungsart**, einen **Gerätenamen** und eine
Online-Anzeige. Zwei Ziele sind wählbar: der `cloud`-Adapter (Datenpunkte unter
`cloud.X.devices.<Gerät>`) oder direkt `vis.0.<Gerät>.<Feld>`.

Die Meldungen laufen auch weiter, wenn die App nicht im Vordergrund ist: ein
WorkManager-Auftrag alle 15 Minuten, ein Alarm, der auch im Doze-Modus auslöst, und —
optional, für Geräte, deren Hersteller Hintergrundarbeit vollständig unterbindet — ein
Vordergrunddienst. Der Tab *Andere* bietet eine Abkürzung zu den
Akkuoptimierungs-Einstellungen an, solange das System die App noch einschränkt.

### Matter

Die App meldet sich als Matter-Commissioner an. Der gescannte QR-Code eines Geräts wird an
den ioBroker-Matter-Adapter übergeben, der das Gerät in deine Installation aufnimmt.

### Geofence

Benannte Orte mit Radius (mindestens 100 m); Betreten oder Verlassen schreibt einen
booleschen Datenpunkt unter `iot.0.app.geofence.<Name>`, den der Adapter bei der ersten
Verwendung anlegt.

### Kiosk- und Wandpanel-Verhalten

Display wachhalten · nach N Sekunden Inaktivität auf einen gewählten Wert dimmen und beim
nächsten Tippen zurückstellen · nach N Sekunden zur Startseite zurückkehren · Ausrichtung
sperren · Statusleiste (mit frei wählbarer Farbe) und Navigationsleiste anzeigen, ausblenden
oder transparent schalten · Vollbild erzwingen · fester oder automatischer Zoom, getrennt für
Hoch- und Querformat · Scrollen und Zoomen erlauben oder sperren.

### Projekte

Bis zu **3 Projekte**, jedes mit eigener Verbindung, Visualisierung und Darstellung. Ein
langer Druck auf das App-Icon bietet je Projekt eine Verknüpfung an; wird die App darüber
gestartet, bleibt sie bis zum Neustart auf diesem Projekt.

### Schutz

Gesichts- oder Fingerabdruckerkennung lässt sich unabhängig voneinander für den App-Start und
für das Öffnen der Einstellungen verlangen.

---

## Einstellungsreferenz

Die Einstellungen öffnen sich mit einem **Drei-Finger-Tipp** auf die Visualisierung und sind
in fünf Tabs gegliedert: **Lokal**, **Cloud**, **App**, **Andere** und **Matter**.

### Lokal

| Einstellung | Bedeutung |
|---|---|
| Host IP:PORT | Adresse der web-Instanz, z. B. `192.168.1.10:8082`. `https://` erlaubt |
| Benutzername / Passwort | ioBroker-Benutzer für den automatischen Login |
| QR-Scanner | Liest einen `iotConfig`-Code und füllt die Felder aus |
| Selbstsignierte Zertifikate akzeptieren | Für lokale HTTPS-Instanzen mit eigenem Zertifikat |

### Cloud

| Einstellung | Bedeutung |
|---|---|
| Cloud-Typ | `Pro` (iobroker.pro) oder `Custom` |
| Cloud-URL | Nur bei `Custom` |
| Benutzername / Passwort | ioBroker.pro-Konto — aktiviert auch Push-Benachrichtigungen |
| WLAN-SSIDs | Kommagetrennte Heimnetze; darin wird die lokale URL genutzt |
| VPN-Erkennung / automatisch bestätigen | Lokale URL verwenden, solange ein VPN aktiv ist — mit oder ohne Rückfrage |

### App

| Einstellung | Bedeutung |
|---|---|
| Anwendung | `vis-2`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`, `habpanel`, `devices` |
| Projekt | Name des vis-Projekts, Standard `main` |
| URL-Postfix | Wird an die URL angehängt, z. B. `#meineStartView` |
| Instanz-ID | Kennzeichnet dieses Gerät für `vis.0.control` (Views umschalten, aktive View erkennen) |

### Andere

| Einstellung | Bedeutung |
|---|---|
| Zoom erlauben / Scrollen erlauben | Gesten in der WebView zulassen oder sperren |
| Zoom (Hochformat) / Zoom (Querformat) | Fester Anfangszoom je Ausrichtung |
| Automatischer Zoom | Setzt `width=device-width`, die Seite skaliert sich selbst |
| Vollbild erzwingen | Setzt `viewport-fit=cover` |
| Neuladen bei Ausrichtungswechsel | Hilft bei Views, die sich nicht sauber neu anordnen |
| Ausrichtung | Auf Hoch- oder Querformat festlegen |
| Statusleiste | Sichtbar, ausgeblendet oder transparent, mit freier Farbe und hellem Text |
| Navigationsleiste | Sichtbar, ausgeblendet oder transparent (nur Android) |
| Display nicht abschalten | Verhindert, dass der Bildschirm ausgeht |
| Dimmen nach Sekunden / Dimmen auf | Nach Inaktivität dimmen, beim nächsten Tippen zurück (`0` = aus) |
| Nach Sekunden zur Startseite | Nach Inaktivität zur Start-View zurück (`0` = aus) |
| Neuladen, wenn die App aktiv wird | Harter Reload beim Zurückkehren aus dem Hintergrund |
| Zwei-Finger-Doppeltipp lädt neu | Reload-Geste aktivieren oder abschalten |
| Telemetrie-Ziel | `cloud`-Adapter oder `vis.0` |
| Akku / Standort / Helligkeit / Gerätename | Welche Werte gemeldet werden |
| Dauerhaft im Hintergrund melden | Vordergrunddienst mit dauerhafter Benachrichtigung, für Geräte, die Hintergrundarbeit blockieren |
| Akkuoptimierung | Abkürzung zur Systemeinstellung |
| Gerätename | Name für die Datenpunkte dieses Geräts |
| Pro-Logo anzeigen | Anzeige in der Ecke, solange die Cloud-Verbindung genutzt wird |
| App-Start schützen / Einstellungen schützen | Biometrische Sperre |
| Sprache / Dunkles Design | App-Sprache (EN/DE/RU) und Erscheinungsbild |

### Matter

Auswahl der Matter-Instanz und der Inbetriebnahme-Dialog.

---

## Gesten

| Geste | Wirkung |
|---|---|
| Drei-Finger-Tipp | Einstellungen öffnen |
| Zwei-Finger-Doppeltipp | Seite neu laden (abschaltbar) |
| Tippen nach dem Dimmen | Vorherige Helligkeit wiederherstellen |
| Langer Druck auf das App-Icon | Ein bestimmtes Projekt starten |

---

## Problembehebung

| Symptom | Ursache / Abhilfe |
|---|---|
| Einstellungen öffnen sich bei jedem Start | Der Verbindungstest ist fehlgeschlagen — IP, Port, Zugangsdaten und ob die web-Instanz läuft prüfen |
| Weiße Seite | Falscher Anwendungstyp oder falscher Projektname; Port prüfen (8082, lovelace 8091) |
| Funktioniert zu Hause, nicht unterwegs | Keine Cloud eingerichtet oder die WLAN-SSID-Liste fehlt, sodass die App weiter die lokale Adresse versucht |
| Landet immer wieder auf der Login-Seite | Zugangsdaten falsch oder der Benutzer hat keine Rechte für die View |
| Widget-Kachel bleibt leer | Siehe [widgets.de.md](widgets.de.md) — meist der `/state/`-Endpunkt des web-Adapters |
| Keine Push-Benachrichtigungen | ioBroker.pro-Zugangsdaten fehlen oder sind ungültig; Push hängt an einem gültigen Pro-Konto |
| Hintergrundwerte bleiben nachts aus | Doze-Modus — App von der Akkuoptimierung ausnehmen oder dauerhaftes Melden im Hintergrund aktivieren |
| Selbstsigniertes Zertifikat wird abgelehnt | *Selbstsignierte Zertifikate akzeptieren* im Tab *Lokal* aktivieren |

---

## Fehler melden

[Ein Issue anlegen](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) und
Android-Version, Gerätemodell, App-Version (unten auf dem Einstellungsbildschirm), verwendete
Visualisierung und Verbindungsart angeben. IP-Adressen, Benutzernamen und Passwörter in
Screenshots unkenntlich machen.
