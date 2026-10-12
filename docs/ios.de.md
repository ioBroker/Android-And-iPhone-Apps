<img src="images/app-icon.png" width="88" align="right" alt="ioBroker Visu App-Icon" />

# ioBroker Visu — iPhone & iPad

[⬅️ Zurück zur Übersicht](../README.de.md) · 🇬🇧 [English version](ios.md)

**📲 [Im App Store installieren](https://apps.apple.com/app/iobroker-visu/id1673095774)**

| | |
|---|---|
| **App-Name** | ioBroker Visu |
| **Bundle-ID** | `com.iobroker.visu` |
| **Anbieter** | ioBroker GmbH |
| **Preis** | Kostenlos — keine Werbung, keine In-App-Käufe |
| **Kategorie** | Lifestyle |
| **Voraussetzung** | iOS / iPadOS 16.1 oder neuer |
| **Geräte** | iPhone, iPad, Mac mit Apple-Silicon |
| **Sprachen** | Englisch, Deutsch, Russisch |
| **Store-Link** | <https://apps.apple.com/app/iobroker-visu/id1673095774> |

> Im App Store gibt es noch eine ältere App, die schlicht **ioBroker** heißt
> ([id1449564305](https://apps.apple.com/app/iobroker/id1449564305)). Sie ist der Vorgänger
> und wird nicht mehr weiterentwickelt. Bitte **ioBroker Visu** installieren.

---

## Screenshots

Die Einstellungen sind in fünf Tabs gegliedert, darüber steht die Projektauswahl:

| Lokal | Pro Cloud | Anwendung |
|---|---|---|
| <img src="images/ios/iphone-01-local.png" width="220" alt="Tab Lokal auf einem iPhone: QR-Scan, Host, Benutzername, Passwort" /> | <img src="images/ios/iphone-02-procloud.png" width="220" alt="Tab Pro Cloud auf einem iPhone: Typ, E-Mail, Passwort, WLAN-SSIDs" /> | <img src="images/ios/iphone-03-application.png" width="220" alt="Tab Anwendung auf einem iPhone: Visualisierung, vis-Projekt, Instanz-ID, URL-Zusatz" /> |

| Sonstige | Matter |
|---|---|
| <img src="images/ios/iphone-04-others.png" width="220" alt="Tab Sonstige auf einem iPhone: Design, Sprache, Gerätename, biometrischer Schutz" /> | <img src="images/ios/iphone-05-matter.png" width="220" alt="Tab Matter auf einem iPhone: Matter-Instanz, Gerät per QR oder Kopplungscode hinzufügen" /> |

Auf dem iPad nutzen dieselben Tabs die volle Breite:

| Lokal | Pro Cloud | Anwendung |
|---|---|---|
| <img src="images/ios/ipad-01-local.png" width="250" alt="Tab Lokal auf einem iPad" /> | <img src="images/ios/ipad-02-procloud.png" width="250" alt="Tab Pro Cloud auf einem iPad" /> | <img src="images/ios/ipad-03-application.png" width="250" alt="Tab Anwendung auf einem iPad" /> |

| Sonstige | Matter |
|---|---|
| <img src="images/ios/ipad-04-others.png" width="340" alt="Tab Sonstige auf einem iPad mit den Karten Allgemein, Sicherheit und Anzeige" /> | <img src="images/ios/ipad-05-matter.png" width="340" alt="Tab Matter auf einem iPad" /> |

*Offizielle App-Store-Screenshots. Die App wird laufend weiterentwickelt, Einzelheiten können
in einer neueren Version abweichen.*

---

## Funktionsumfang

Die App zeigt die Visualisierung, die ohnehin schon auf deiner ioBroker-Installation läuft, in
einer darauf abgestimmten Vollbild-`WKWebView` und ergänzt alles, was Safari nicht kann: eine
gespeicherte Verbindung, automatisches Umschalten zwischen lokal und extern,
Homescreen-Widgets, Push-Benachrichtigungen, Gerätesensoren, Matter-Inbetriebnahme und
Kiosk-Verhalten.

Die iOS- und die Android-App teilen sich ein Einstellungsmodell, jede Option bedeutet auf
beiden dasselbe — die Unterschiede stehen unter [Unterschiede zu
Android](#unterschiede-zu-android).

### Unterstützte Visualisierungen

`vis-2` · `devices` · `vis` · `lovelace` · `material` · `jarvis` · `iQontrol` · `habpanel` · `aura`

Die Auswahl bestimmt lediglich, welche URL die App öffnet — alles andere, was deine
web-Instanz ausliefert, lässt sich ebenfalls verwenden. Standardport ist **8082**, außer bei
`lovelace`: dort **8091**.

### Verbindung

- **Lokal** — IP und Port der web-Instanz, z. B. `192.168.1.10:8082`. Ein reines `IP:PORT`
  wird automatisch vervollständigt, `https://` kann explizit angegeben werden. Benutzername
  und Passwort führen optional einen automatischen Login durch. Unter dem Feld steht die
  Adresse, die die App tatsächlich öffnet — mit Schema, Port und Pfad. Seit iOS 14 braucht
  eine lokale Adresse außerdem die Berechtigung *Lokales Netzwerk*; ist sie aus, sagt der Tab
  *Lokal* das, statt einen Server zu melden, der nicht antwortet.
- **Pro-Cloud** — dein [ioBroker.pro](https://iobroker.pro)-Konto für den Zugriff von außen.
  Das Abonnement wird gegen die Cloud geprüft; auf Wunsch zeigt ein Pro-Logo in der Ecke an,
  dass gerade die Cloud-Verbindung genutzt wird.
- **Eigene Cloud** — statt ioBroker.pro eine beliebige selbst betriebene URL. Die Plakette in
  der Ecke zeigt dann `remote` statt `.pro`.
- **WLAN-SSIDs** — kommagetrennte Liste deiner Heimnetze. Solange eines davon verbunden ist,
  nutzt die App die lokale URL, sonst die Cloud. iOS verrät den WLAN-Namen nur mit
  Standortberechtigung; solange er nicht lesbar ist, fragt die App die lokale Installation, ob
  sie antwortet, statt in die Cloud zu wechseln.
- **Selbstsignierte Zertifikate** — je Projekt (Tab *Sonstige*) für lokale HTTPS-Instanzen
  erlaubbar. Ein abgelehntes Zertifikat wird benannt, statt als „keine Verbindung“ gemeldet.
- **QR-Code-Einrichtung** — im Tab *Lokal* liest ein Scanner den von ioBroker erzeugten
  `iotConfig`-Code und füllt Port, IP, Cloud-Benutzer und Passwort in einem Schritt aus.
- **Sitzungswiederherstellung** — eine abgelaufene Sitzung erzeugt keinen Fehler, sondern nur
  eine Weiterleitung auf eine Login-Seite. Die App erneuert das Sitzungs-Cookie vor Ablauf,
  erneuert es erneut beim Zurückkehren in den Vordergrund und erkennt eine Login-Seite an
  ihrer URL, meldet sich still neu an und kehrt zur vorherigen Seite zurück. Genau das hält
  ein fest montiertes iPad angemeldet.

### Homescreen-Widgets

Zwei Kacheltypen — ein **Toggle**, der einen Datenpunkt schaltet, und eine **Analog**-Kachel,
die einen Zahlenwert anzeigt. Es gibt sie in zwei Ausprägungen: ein **Übersichts**-Widget, das
die ersten konfigurierten Kacheln zeigt und auf jedem unterstützten System läuft, und ein
**Einzel**-Widget für eine ausgewählte Kachel, das iOS 17 voraussetzt.

➡️ **[widgets.de.md](widgets.de.md) — wie Widgets aktualisiert werden und was dafür
einzurichten ist.**

### Push-Benachrichtigungen

Aus ioBroker gesendete Nachrichten (`iot.0.app.message`, optional mit `app.title`,
`app.expire` und `app.priority`) kommen als iOS-Benachrichtigung mit Aktionsknöpfen an; die
gedrückte Aktion wird nach ioBroker zurückgeschrieben. Eine Benachrichtigung kann gezielt
bestimmte Geräte ansprechen und eine zu öffnende URL mitführen. Push setzt ein gültiges
ioBroker.pro-Konto voraus.

### Gerätedaten (Telemetrie)

Die App kann nach ioBroker zurückmelden: **Akkustand** und Ladezustand,
**Bildschirmhelligkeit** (in beide Richtungen — ein Schreiben auf den Datenpunkt dimmt das
Gerät), **Standort**, **WLAN-SSID**, **Verbindungsart**, einen **Gerätenamen** und eine
Online-Anzeige. Zwei Ziele sind wählbar: der `cloud`-Adapter (Datenpunkte unter
`cloud.X.devices.<Gerät>`) oder direkt `vis.0.<Gerät>.<Feld>`.

Solange die Visualisierung auf dem Bildschirm ist, meldet die App alle 45 Sekunden über deren
Verbindung. Im Hintergrund führt `BGTaskScheduler` etwa alle 15 Minuten eine Runde aus — den
genauen Zeitpunkt bestimmt iOS, der Takt ist also ein Ziel und keine Zusage. Für ein Gerät,
das durchgehend melden muss, gibt es einen optionalen Modus, der den Prozess über
Standort-Updates am Leben hält; er kostet die Standortberechtigung „Immer“ und die sichtbare
Standortanzeige.

### Mikrofon, Kamera und Ton

Eine Seite darf Mikrofon und Kamera nutzen — zum Beispiel ein Gegensprech- oder
Türklingel-Widget. iOS fragt einmal nach der Berechtigung; WebKit fragt nicht bei jedem Laden
der Seite erneut. Töne dürfen ohne vorheriges Tippen abspielen, damit ein Klingelton auch auf
einem Display zu hören ist, das niemand berührt hat.

> WebKit bietet Mikrofon und Kamera nur Seiten an, die über **HTTPS** geladen sind
> (ioBroker.pro oder eine lokale Instanz mit Zertifikat). Über reines `http://<ip>` kann eine
> Seite sie nicht nutzen; Töne abspielen geht in beiden Fällen.

### Fernsteuerung (REST-Schnittstelle, kompatibel mit Fully Kiosk)

ioBroker kann auf dem iPad einen Ton abspielen, Text sprechen, die Helligkeit setzen oder eine
Seite öffnen — über dieselbe REST-Schnittstelle wie die Android-App, also die von **Fully Kiosk
Browser**. Der Adapter [ioBroker.fullybrowser](https://github.com/arteck/ioBroker.fullybrowser)
funktioniert damit unverändert.

> **Nur, solange die App sichtbar ist.** iOS friert eine App kurz nach dem Verlassen des
> Bildschirms ein und lässt keine App dauerhaft einen Server im Hintergrund betreiben. Für ein
> Wand-iPad *Display anlassen* einschalten und die App vorne halten, z. B. mit dem *geführten
> Zugriff*. Ein gesperrtes iPad kann keine App aufwecken.

**Einrichten:** *Sonstige* → *Fernsteuerung*: REST-Schnittstelle einschalten, Passwort setzen,
speichern. Die Karte zeigt die Adresse, z. B. `http://192.168.1.30:2323`. In ioBroker.fullybrowser
das Gerät mit Protokoll `http`, dieser IP, Port `2323` und dem Passwort eintragen. Im Browser ohne
Passwort geöffnet, zeigt die Adresse eine Seite zum Ausprobieren der Befehle.

```
http://192.168.1.30:2323/?cmd=textToSpeech&text=Es%20klingelt&locale=de_DE&password=…&type=json
http://192.168.1.30:2323/?cmd=playSound&url=http%3A%2F%2F192.168.1.10%3A8082%2Fding.mp3&password=…
```

| Befehl | Parameter | iOS |
|---|---|---|
| `deviceInfo` / `listSettings` | | Akku, Helligkeit, aktuelle Seite, IP, Lautstärke … als JSON |
| `textToSpeech` / `stopTextToSpeech` | `text=`, `locale=de_DE`, `queue=1` | ✅ auch bei eingeschaltetem Stummschalter |
| `playSound` / `stopSound` | `url=`, `loop=true` | ✅ MP3 oder WAV von einer URL, auch bei Stummschalter |
| `setStringSetting` | `key=screenBrightness&value=0…255` | ✅ bleibt über Neustarts erhalten |
| `startScreensaver` / `stopScreensaver` / `triggerMotion` | | ✅ dimmen / zurückstellen |
| `screenOff` / `screenOn` | | ⚠️ schwarzer Bildschirm mit minimaler Helligkeit und zurück — das Panel bleibt an |
| `loadURL` / `loadStartURL` / `refreshTab` / `restartApp` | `url=` | ✅ |
| `setOverlayMessage` / `showToast` | `text=` | ✅ |
| `getScreenshot` | | ✅ PNG der Seite |
| `clearCache` / `clearCookies` / `clearWebstorage` | | ✅ |
| `vibrate` | | nur iPhone |
| `setAudioVolume`, `toBackground`, `exitApp`, `startApplication`, `setBooleanSetting` | | ❌ `Not supported on iOS` |

### Matter

Die App bringt eine Apple-`MatterSupport`-Erweiterung zur Geräteeinrichtung mit. Der
gescannte QR-Code eines Geräts wird an den ioBroker-Matter-Adapter übergeben, der das Gerät in
deine Installation aufnimmt.

### Geofence

Benannte Orte mit Radius; Betreten oder Verlassen schreibt einen booleschen Datenpunkt unter
`iot.0.app.geofence.<Name>`, den der Adapter bei der ersten Verwendung anlegt. Der Radius wird
eingetippt — mindestens 100 m, höchstens, was das Gerät überwachen kann —, die Koordinaten
lassen sich eintippen oder auf der Karte setzen. Ein neuer Ort meldet seinen Zustand sofort,
der Datenpunkt erscheint also, ohne den Ort erst verlassen zu müssen.

### Kiosk- und Wandpanel-Verhalten

Display wachhalten · nach N Sekunden Inaktivität auf einen gewählten Wert dimmen und beim
nächsten Tippen zurückstellen · nach N Sekunden zur Startseite zurückkehren · Ausrichtung
sperren · Statusleiste (mit frei wählbarer Farbe) anzeigen, ausblenden oder transparent
schalten · Home-Indikator ausblenden · Vollbild erzwingen · fester Zoom mit zwei
Nachkommastellen (z. B. `1.15`), getrennt für Hoch- und Querformat und sofort beim Drehen
angewendet, oder automatischer Zoom · Scrollen und Zoomen erlauben oder sperren.

### Projekte

Bis zu **3 Projekte**, jedes mit eigener Verbindung, Visualisierung und Darstellung. Ein
langer Druck auf das App-Icon bietet je Projekt eine Quick Action an; wird die App darüber
gestartet, bleibt sie bis zum Neustart auf diesem Projekt.

### Schutz

Face ID / Touch ID lässt sich unabhängig voneinander für den App-Start und für das Öffnen der
Einstellungen verlangen.

---

## Einstellungsreferenz

Die Einstellungen öffnen sich mit einem **Drei-Finger-Tipp** auf die Visualisierung und sind
in fünf Tabs gegliedert: **Lokal**, **Pro Cloud**, **Anwendung**, **Sonstige** und
**Matter**. Die Projektauswahl steht über den Tabs.

### Lokal

| Einstellung | Bedeutung |
|---|---|
| Host IP:PORT | Adresse der web-Instanz, z. B. `192.168.1.10:8082`. `https://` erlaubt |
| Benutzername / Passwort | ioBroker-Benutzer für den automatischen Login |
| QR-Scanner | Liest einen `iotConfig`-Code und füllt die Felder aus |
| Verwendete Adresse | Steht unter dem Feld: die vollständige Adresse, die die App öffnet |

### Pro-Cloud

| Einstellung | Bedeutung |
|---|---|
| Cloud-Typ | `Pro` (iobroker.pro) oder `Custom` |
| Cloud-URL | Nur bei `Custom` |
| Benutzername / Passwort | ioBroker.pro-Konto — aktiviert auch Push-Benachrichtigungen |
| WLAN-SSIDs | Kommagetrennte Heimnetze; darin wird die lokale URL genutzt |

### Anwendung

| Einstellung | Bedeutung |
|---|---|
| Anwendung | `vis-2`, `devices`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`, `habpanel`, `aura` |
| Projekt | Name des vis-Projekts, Standard `main`. Die Projekte der Installation werden angeboten; gibt es nur eines, wird es gewählt |
| URL-Postfix | Wird an die URL angehängt, z. B. `#meineStartView` |
| Instanz-ID | Kennzeichnet dieses Gerät für `vis.0.control` (Views umschalten, aktive View erkennen) |

### Sonstige

Gegliedert in die Karten **Allgemein**, **Sicherheit**, **Anzeige** und **Verhalten**:

| Einstellung | Karte | Bedeutung |
|---|---|---|
| Design | Allgemein | System, hell oder dunkel |
| Sprache | Allgemein | App-Sprache: System, Englisch, Deutsch, Russisch |
| Gerätename | Allgemein | Name für die Datenpunkte dieses Geräts |
| App-Start schützen | Sicherheit | Beim Start nach Face ID oder Touch ID fragen |
| Einstellungen schützen | Sicherheit | Vor dem Öffnen dieser Einstellungen erneut fragen |
| Statusleiste | Anzeige | Anzeigen, ausblenden oder transparent |
| Helle Statusleisten-Schrift | Anzeige | Helle Schrift für dunkle Statusleisten |
| Statusleisten-Farbe | Anzeige | Freie Farbe über den Farbwähler |
| Home-Indikator ausblenden | Anzeige | Blendet den Balken am unteren Rand aus, solange der Bildschirm nicht berührt wird |
| Ausrichtung | Anzeige | Automatisch oder auf Hoch- bzw. Querformat festgelegt |

Die Karte **Verhalten** enthält den Rest — wie die Ansicht auf dich reagiert:

| Einstellung | Bedeutung |
|---|---|
| Zoom erlauben / Scrollen erlauben | Gesten in der WebView zulassen oder sperren |
| Zoom (Hochformat) / Zoom (Querformat) | Fester Anfangszoom je Ausrichtung, mit zwei Nachkommastellen |
| Automatischer Zoom | Setzt `width=device-width`, die Seite skaliert sich selbst |
| Vollbild erzwingen | Setzt `viewport-fit=cover` |
| Neuladen bei Ausrichtungswechsel | Hilft bei Views, die sich nicht sauber neu anordnen |
| Pull-to-Refresh | Reload-Geste aktivieren oder abschalten |
| Display nicht abschalten | Verhindert, dass der Bildschirm ausgeht |
| Dimmen nach Sekunden / Dimmen auf | Nach Inaktivität dimmen, beim nächsten Tippen zurück (`0` = aus) |
| Nach Sekunden zur Startseite | Nach Inaktivität zur Start-View zurück (`0` = aus) |
| Neuladen, wenn die App aktiv wird | Harter Reload beim Zurückkehren aus dem Hintergrund (unter iOS standardmäßig an) |
| Pro-Logo anzeigen | Anzeige in der Ecke, solange die Cloud-Verbindung genutzt wird |
| Telemetrie-Ziel | `cloud`-Adapter oder `vis.0` |
| Akku / Standort / Helligkeit | Welche Gerätewerte gemeldet werden |
| Dauerhaft im Hintergrund melden | Hält das Melden über Standort-Updates am Leben; benötigt die Berechtigung „Immer“ |
| Selbstsignierte Zertifikate akzeptieren | Für lokale HTTPS-Instanzen mit eigenem Zertifikat |
| REST-Schnittstelle | An/aus, Port, Passwort — siehe [Fernsteuerung](#fernsteuerung-rest-schnittstelle-kompatibel-mit-fully-kiosk) |

### Matter

Auswahl der Matter-Instanz und der Inbetriebnahme-Dialog.

---

## Gesten

| Geste | Wirkung |
|---|---|
| Drei-Finger-Tipp | Einstellungen öffnen |
| Nach unten ziehen | Seite neu laden — nur, wenn die Seite bereits ganz oben steht |
| Tippen nach dem Dimmen | Vorherige Helligkeit wiederherstellen |
| Langer Druck auf das App-Icon | Ein bestimmtes Projekt starten (Quick Action) |

Über der allerersten Visualisierung zeigt die App einmalig einen kurzen Hinweis auf den
Drei-Finger-Tipp. Eine Visualisierung kann die Einstellungen auch selbst öffnen — der
verlässliche Weg auf einem Wanddisplay, auf dem drei Finger umständlich sind:

```js
window.ReactNativeWebView.postMessage(JSON.stringify({ command: 'openSettings' }));
```

---

## Unterschiede zu Android

| Thema | iOS |
|---|---|
| Interaktive Widgets | Das Schreiben direkt von der Kachel braucht iOS 17. Unter iOS 16 öffnet ein Tipp die App, die dann schreibt |
| Reload-Geste | Nach unten ziehen statt Zwei-Finger-Doppeltipp |
| Navigationsleiste | Gibt es unter iOS nicht; die Einstellung blendet stattdessen den Home-Indikator aus. iOS blendet ihn nur ab — eine Berührung holt ihn kurz zurück |
| Mehrere Visualisierungen in einem Projekt | Bisher nur unter Android — unter iOS zeigt ein Projekt eine Visualisierung |
| Fernsteuerung (REST-Schnittstelle, kompatibel mit Fully Kiosk) | Nur, solange die App sichtbar ist — iOS lässt keine App dauerhaft einen Server im Hintergrund betreiben. Keine System-Lautstärke, kein Wecken eines gesperrten Bildschirms, kein Starten anderer Apps |
| Hintergrundmeldungen | `BGTaskScheduler`; iOS bestimmt den Takt, eine Runde alle 15 Minuten ist nicht garantiert |
| Matter | Apples `MatterSupport`-Erweiterung statt Google Play Services |
| VPN-Erkennung | Nicht verfügbar — iOS lässt Apps den VPN-Zustand weder lesen noch steuern |

---

## Problembehebung

| Symptom | Ursache / Abhilfe |
|---|---|
| Einstellungen öffnen sich bei jedem Start | Der Verbindungstest ist fehlgeschlagen — IP, Port, Zugangsdaten und ob die web-Instanz läuft prüfen |
| Weiße Seite | Falscher Anwendungstyp oder falscher Projektname; Port prüfen (8082, lovelace 8091) |
| Funktioniert zu Hause, nicht unterwegs | Keine Cloud eingerichtet oder die WLAN-SSID-Liste fehlt, sodass die App weiter die lokale Adresse versucht |
| Landet immer wieder auf der Login-Seite | Zugangsdaten falsch oder der Benutzer hat keine Rechte für die View |
| Lokale Verbindung scheitert, obwohl Safari die Adresse erreicht | Die Berechtigung *Lokales Netzwerk* ist aus — Einstellungen → Datenschutz & Sicherheit → Lokales Netzwerk → ioBroker Visu |
| „SSL-Fehler“ statt der Seite | Das Zertifikat ist selbstsigniert oder für einen anderen Namen ausgestellt — *Selbstsignierte Zertifikate akzeptieren* im Tab *Sonstige* aktivieren |
| Mikrofon oder Kamera gehen in der Seite nicht | Nur über HTTPS verfügbar — siehe [Mikrofon, Kamera und Ton](#mikrofon-kamera-und-ton) |
| Ziehen nach unten lädt nicht neu | So gewollt — die Geste greift nur, wenn die Seite schon ganz oben steht, damit das Hochscrollen einer langen View nicht neu lädt |
| Widget-Kachel bleibt leer | Siehe [widgets.de.md](widgets.de.md) — meist der `/state/`-Endpunkt des web-Adapters |
| Einzel-Widget wird nicht angeboten | Es braucht iOS 17; unter iOS 16 das Übersichts-Widget verwenden |
| Keine Push-Benachrichtigungen | ioBroker.pro-Zugangsdaten fehlen oder sind ungültig; Push hängt an einem gültigen Pro-Konto |
| Hintergrundwerte kommen unregelmäßig | Unter iOS normal — das System legt die Zeitpunkte der Hintergrundrunden fest |

---

## Fehler melden

[Ein Issue anlegen](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) und
iOS-Version, Gerätemodell, App-Version (unten auf dem Einstellungsbildschirm), verwendete
Visualisierung und Verbindungsart angeben. IP-Adressen, Benutzernamen und Passwörter in
Screenshots unkenntlich machen.
