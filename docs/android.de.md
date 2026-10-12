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

`vis-2` · `devices` · `vis` · `lovelace` · `material` · `jarvis` · `iQontrol` · `habpanel` · `aura`

Die Auswahl bestimmt lediglich, welche URL die App öffnet — alles andere, was deine
web-Instanz ausliefert, lässt sich ebenfalls verwenden. Standardport ist **8082**, außer bei
`lovelace`: dort **8091**.

### Mehrere Visualisierungen in einem Projekt

Ein Projekt kann mehr als eine Visualisierung anbieten — etwa `vis-2` für die Räume und
`lovelace` für die Energieansicht. Bei mehr als einer erscheint über der Seite eine Leiste mit
Tabs. Jeder Tab behält seine eigene Seite: Beim Zurückwechseln sind View, Scrollposition und
Verbindung noch da, und geladen wird ein Tab erst, wenn er zum ersten Mal geöffnet wird.
*Zurück* geht durch den Seitenverlauf, dann zum ersten Tab und erst danach aus der App; die
Inaktivitäts-Rückkehr führt zum ersten Tab und seiner Startseite.

### Verbindung

- **Lokal** — IP und Port der web-Instanz, z. B. `192.168.1.10:8082`. Ein reines `IP:PORT`
  wird automatisch vervollständigt, `https://` kann explizit angegeben werden. Benutzername
  und Passwort führen optional einen automatischen Login durch. Unter dem Feld steht die
  Adresse, die die App tatsächlich öffnet — mit Schema, Port und Pfad.
- **Pro-Cloud** — dein [ioBroker.pro](https://iobroker.pro)-Konto für den Zugriff von außen.
  Das Abonnement wird gegen die Cloud geprüft; auf Wunsch zeigt ein Pro-Logo in der Ecke an,
  dass gerade die Cloud-Verbindung genutzt wird.
- **Eigene Cloud** — statt ioBroker.pro eine beliebige selbst betriebene URL. Die Plakette in
  der Ecke zeigt dann `remote` statt `.pro`.
- **WLAN-SSIDs** — kommagetrennte Liste deiner Heimnetze. Solange eines davon verbunden ist,
  nutzt die App die lokale URL, sonst die Cloud. Android verrät einer App den WLAN-Namen nur
  mit Standortberechtigung *und* eingeschaltetem Standort; der Tab *Remote* sagt, was davon
  fehlt. Solange der Name nicht lesbar ist, fragt die App die lokale Installation, ob sie
  antwortet, statt in die Cloud zu wechseln.
- **VPN-Erkennung** — ist ein VPN aktiv, kann die App die lokale URL vorschlagen oder still
  verwenden, weil die lokale Adresse durch den Tunnel wieder erreichbar ist.
- **QR-Code-Einrichtung** — im Tab *Lokal* liest ein Scanner den von ioBroker erzeugten
  `iotConfig`-Code und füllt Port, IP, Cloud-Benutzer und Passwort in einem Schritt aus.
- **Selbstsignierte Zertifikate** — je Projekt (Tab *Andere*) für lokale HTTPS-Instanzen
  erlaubbar. Die Ausnahme gilt für die Seite, den Login, den Verbindungstest und die Liste der
  vis-Projekte gleichermaßen, nie aber für iobroker.pro. Ein abgelehntes Zertifikat wird
  benannt — nicht vertrauenswürdig, für einen anderen Namen ausgestellt, abgelaufen oder noch
  nicht gültig — statt einer weißen Seite oder „keine Verbindung“.
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

### Mikrofon, Kamera und Ton

Eine Seite darf Mikrofon und Kamera nutzen — zum Beispiel ein Gegensprech- oder
Türklingel-Widget. Die App fragt die Android-Berechtigung ab, wenn eine Seite sie zum ersten
Mal braucht, nicht schon beim Start. Töne dürfen ohne vorheriges Tippen abspielen, damit ein
Klingelton auch auf einem Display zu hören ist, das niemand berührt hat.

> Die Android-WebView bietet Mikrofon und Kamera nur Seiten an, die über **HTTPS** geladen sind
> (ioBroker.pro oder eine lokale Instanz mit Zertifikat). Über reines `http://<ip>` kann eine
> Seite sie nicht nutzen; Töne abspielen geht in beiden Fällen.

### Fernsteuerung (REST-Schnittstelle, kompatibel mit Fully Kiosk)

Die App kann die REST-Schnittstelle von **Fully Kiosk Browser** beantworten, sodass ioBroker ein
Wandtablet steuern kann: Display an- und ausschalten, Klingelton abspielen, Text sprechen,
Helligkeit und Lautstärke setzen, eine Seite öffnen. Der Adapter
[ioBroker.fullybrowser](https://github.com/arteck/ioBroker.fullybrowser) funktioniert damit
unverändert.

**Einrichten**

1. *Andere* → *Fernsteuerung*: REST-Schnittstelle einschalten, Passwort setzen, speichern. Die
   Karte zeigt die Adresse, z. B. `http://192.168.1.20:2323`.
2. In ioBroker.fullybrowser das Gerät mit Protokoll `http`, dieser IP, Port `2323` und dem
   Passwort eintragen.
3. *Über anderen Apps einblenden* erlauben (Knopf auf derselben Karte). Ohne diese Berechtigung
   lässt Android `screenOn` und `toForeground` die App nicht aus dem Hintergrund zurückholen.

Die Schnittstelle läuft auch bei ausgeschaltetem Display weiter — als Vordergrunddienst mit
dauerhafter Benachrichtigung — und startet nach einem Neustart des Geräts von selbst.

**Selbst aufrufen** — beide Adressformen von Fully funktionieren, z. B. aus einem Skript oder
Blockly:

```
http://192.168.1.20:2323/?cmd=textToSpeech&text=Es%20klingelt&password=…&type=json
http://192.168.1.20:2323/screenOn?password=…
```

Jeder Befehl antwortet mit `{"status":"OK"|"Error","statustext":"…"}`; fehlt das Passwort oder
ist es falsch, kommt `Please login`. Im Browser ohne Passwort geöffnet, zeigt die Adresse eine
kleine Seite mit Passwortfeld und einigen Befehlen zum Ausprobieren.

| Befehl | Parameter | Wirkung |
|---|---|---|
| `deviceInfo` | | Akku, Display-Zustand und -Helligkeit, aktuelle Seite, IP, Speicher, Lautstärke, Lichtsensor … als JSON |
| `listSettings` | | `screenBrightness`, `motionDetection`, `startURL` |
| `screenOn` / `screenOff` | | Display wecken / schwarzer Bildschirm (siehe unten) |
| `startScreensaver` / `stopScreensaver` | | Dimmen / zurückstellen, wie nach Inaktivität |
| `triggerMotion` | | Wie eine Berührung: Helligkeit zurück, Display wecken |
| `setStringSetting` | `key=screenBrightness&value=0…255` | Display-Helligkeit; `-1` = die des Systems |
| `setBooleanSetting` | `key=motionDetection&value=true` | Display bei Annäherung wecken (Näherungssensor) |
| `loadURL` / `loadStartURL` / `refreshTab` | `url=` | Seite öffnen / Startseite / neu laden |
| `playSound` / `stopSound` | `url=`, `loop=true`, `stream=3` | MP3- oder WAV-Datei von einer URL abspielen |
| `setAudioVolume` | `level=0…100`, `stream=3` | Lautstärke eines Audio-Kanals |
| `textToSpeech` / `stopTextToSpeech` | `text=`, `locale=de_DE`, `queue=1` | Text sprechen |
| `setOverlayMessage` | `text=` | Meldung über der Seite; leerer Text entfernt sie |
| `showToast` / `vibrate` | `text=` / `millis=` | Kurze Meldung / Vibration |
| `toForeground` / `toBackground` / `restartApp` / `exitApp` | | App-Steuerung |
| `startApplication` | `package=` | Eine andere App öffnen |
| `getScreenshot` | | Bildschirmfoto als PNG |
| `clearCache` / `clearCookies` / `clearWebstorage` | | Web-Daten löschen |

Kiosk-Sperre, Kamerabilder und Videos werden nicht unterstützt und antworten mit
`Not supported`.

> **Display aus ohne Administratorrechte:** Eine App darf das Panel nicht selbst abschalten.
> `screenOff` zeigt einen schwarzen Bildschirm mit minimaler Hintergrundbeleuchtung und
> überlässt das Abschalten dem Bildschirm-Timeout des Systems; eine Berührung oder `screenOn`
> holt die Seite zurück. Status- und Navigationsleiste bleiben sichtbar, solange sie auf
> *anzeigen* stehen.

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
oder transparent schalten · Vollbild erzwingen · fester Zoom mit zwei Nachkommastellen
(z. B. `1.15`), getrennt für Hoch- und Querformat und sofort beim Drehen angewendet, oder
automatischer Zoom · Scrollen und Zoomen erlauben oder sperren · Fernsteuerung durch ioBroker
über die [REST-Schnittstelle](#fernsteuerung-rest-schnittstelle-kompatibel-mit-fully-kiosk).

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
| Verwendete Adresse | Steht unter dem Feld: die vollständige Adresse, die die App öffnet |

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
| Anwendungen | Welche Visualisierungen das Projekt anbietet: `vis-2`, `devices`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`, `habpanel`, `aura`. Mehrere werden zu [Tabs](#mehrere-visualisierungen-in-einem-projekt) |
| Projekt | Name des vis-Projekts, Standard `main`. Die Projekte der Installation werden angeboten; gibt es nur eines, wird es gewählt |
| URL-Postfix | Wird an die URL angehängt, z. B. `#meineStartView` |
| Instanz-ID | Kennzeichnet dieses Gerät für `vis.0.control` (Views umschalten, aktive View erkennen) |

Jede Anwendung hat eine eigene Karte mit diesen Feldern; die Pfeile in ihrer Überschrift
verschieben sie in der Tab-Reihenfolge.

### Andere

| Einstellung | Bedeutung |
|---|---|
| Zoom erlauben / Scrollen erlauben | Gesten in der WebView zulassen oder sperren |
| Zoom (Hochformat) / Zoom (Querformat) | Fester Anfangszoom je Ausrichtung, mit zwei Nachkommastellen |
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
| Selbstsignierte Zertifikate akzeptieren | Für lokale HTTPS-Instanzen mit eigenem Zertifikat |
| REST-Schnittstelle | An/aus, Port, Passwort, Wecken bei Annäherung — siehe [Fernsteuerung](#fernsteuerung-rest-schnittstelle-kompatibel-mit-fully-kiosk) |

### Matter

Auswahl der Matter-Instanz und der Inbetriebnahme-Dialog.

---

## Gesten

| Geste | Wirkung |
|---|---|
| Drei-Finger-Tipp | Einstellungen öffnen |
| Zwei-Finger-Doppeltipp | Seite neu laden (abschaltbar) |
| Tippen nach dem Dimmen | Vorherige Helligkeit wiederherstellen |
| Tippen auf den schwarzen Bildschirm | Zurück aus `screenOff` der REST-Schnittstelle |
| Langer Druck auf das App-Icon | Ein bestimmtes Projekt starten |

Über der allerersten Visualisierung zeigt die App einmalig einen kurzen Hinweis auf den
Drei-Finger-Tipp. Eine Visualisierung kann die Einstellungen auch selbst öffnen — der
verlässliche Weg auf einem Wanddisplay, auf dem drei Finger umständlich sind:

```js
window.ReactNativeWebView.postMessage(JSON.stringify({ command: 'openSettings' }));
```

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
| „SSL-Fehler“ statt der Seite | Das Zertifikat ist selbstsigniert oder für einen anderen Namen ausgestellt — *Selbstsignierte Zertifikate akzeptieren* im Tab *Andere* aktivieren |
| Heimnetz wird nicht erkannt | Zum Lesen des WLAN-Namens braucht es Standortberechtigung und eingeschalteten Standort — der Tab *Remote* sagt, was fehlt |
| Mikrofon oder Kamera gehen in der Seite nicht | Nur über HTTPS verfügbar — siehe [Mikrofon, Kamera und Ton](#mikrofon-kamera-und-ton) |
| `screenOn` / `toForeground` antworten mit einem Fehler | Für die App *Über anderen Apps einblenden* erlauben (Knopf auf der Karte *Fernsteuerung*) |

---

## Fehler melden

[Ein Issue anlegen](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) und
Android-Version, Gerätemodell, App-Version (unten auf dem Einstellungsbildschirm), verwendete
Visualisierung und Verbindungsart angeben. IP-Adressen, Benutzernamen und Passwörter in
Screenshots unkenntlich machen.
