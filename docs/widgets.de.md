# Homescreen-Widgets

[⬅️ Zurück zur Übersicht](../README.de.md) · 🇬🇧 [English version](widgets.md)

Ein Homescreen-Widget ist eine Kachel auf dem Startbildschirm des Telefons oder Tablets, die
einen ioBroker-Datenpunkt anzeigt und — wenn er beschreibbar ist — verändert, **ohne die App
zu öffnen**.

> *Widget* bedeutet in der ioBroker-Welt zweierlei. Ein **vis-Widget** ist ein Element
> innerhalb deiner Visualisierung. Diese Seite beschreibt das **Homescreen-Widget** des
> mobilen Betriebssystems. Die beiden haben nichts miteinander zu tun.

---

## Die zwei Kacheltypen

| | Toggle | Analog |
|---|---|---|
| **Zweck** | Einen Datenpunkt ein-/ausschalten oder einen festen Wert schreiben | Einen Zahlenwert anzeigen |
| **Typische Datenpunkte** | `switch`, `button`, boolesche Werte | Temperatur, Leistung, Akku, Luftfeuchte |
| **Darstellung** | Icon, Beschriftung, Farbe für aktiv/inaktiv | Zahl mit Einheit, Halbkreis-Tacho, waagerechter Balken, senkrechter Balken |
| **Tippen** | Schreibt sofort — auf Wunsch nach einem Bestätigungsdialog | Beschreibbarer Datenpunkt: Schieberegler-Dialog. Nur lesbarer: aktualisiert den Wert |

Beide passen sich der Größe an — Icon, Beschriftung, Wert und Tacho skalieren mit der Größe,
auf die du die Kachel ziehst — und lassen sich nach dem Platzieren neu konfigurieren. Tacho-
und Balkendarstellung werden nur angeboten, wenn der Datenpunkt die Einheit `%` trägt oder
`common.min` **und** `common.max` gesetzt sind — ohne Wertebereich hat ein Balken nichts zu
füllen.

---

## Wie ein Widget zu seinem Wert kommt — das Aktualisierungsprinzip

Ein Widget ist ein eigener Prozess, getrennt von der App. Es nutzt **nicht** die WebView und
**nicht** den vis-Socket — die Visualisierung muss nicht einmal geöffnet sein. Stattdessen
spricht das Widget schlichtes REST mit deiner ioBroker-Installation:

| Zweck | Anfrage |
|---|---|
| Datenpunkt lesen | `GET {base}/state/{id}` |
| Datenpunkt schreiben | `POST {base}/state/{id}` mit Body `{"val": …}` |
| Objektbaum durchsuchen | `GET {base}/objects?pattern=…` |

`{base}` wird **zuerst lokal, dann über die Cloud** aufgelöst: Das Widget versucht die lokale
URL des Projekts mit 3 Sekunden Zeitlimit und greift erst bei einem Fehlschlag auf die Cloud
des Projekts zurück (`https://iobroker.pro` oder deine eigene URL) mit 5 Sekunden Zeitlimit.
Deshalb funktioniert dieselbe Kachel zu Hause und im Mobilfunknetz. Die Zugangsdaten gehen als
HTTP-Basic-Auth mit — die lokalen beim lokalen Versuch, die Pro-Zugangsdaten beim
Cloud-Versuch.

Jedes Widget merkt sich, zu welchem **Projekt** es gehört, und benutzt immer dessen URL und
Zugangsdaten.

### Die vier Wege, auf denen eine Kachel aktuell wird

**1. Push — sofort, der Normalfall.**
Die ioBroker-Cloud schickt eine Nachricht mit `id`, `value` und `ack`. Die App empfängt sie
auch im Hintergrund oder geschlossen, speichert den Wert für **jedes** Widget, dessen
Datenpunkt-ID passt, und erzwingt ein Neuzeichnen der Kachel. Genau das lässt eine
Lampen-Kachel innerhalb einer Sekunde umspringen, wenn jemand die Lampe anderswo schaltet.
Push setzt ein gültiges **ioBroker.pro**-Konto voraus — siehe Voraussetzungen unten.

**2. Neuzeichnen — das 60-Sekunden-Sicherheitsnetz (Android).**
Immer wenn der Launcher die Kachel neu zeichnen lässt, prüft das Widget das Alter seines
zwischengespeicherten Werts. Gibt es noch keinen oder ist er älter als 60 Sekunden, liest es
den Datenpunkt vor dem Zeichnen neu. Eine Kachel, die wieder ins Blickfeld kommt, ist damit
nie älter als eine Minute.

**3. Automatische Aktualisierung — Abfrage im Intervall, standardmäßig aus.**
Je Widget einstellbar: **aus (nur Push) / alle 15 Minuten / alle 30 Minuten / jede Stunde**.
Unter Android läuft ein einziger WorkManager-Auftrag im kürzesten Intervall, das irgendein
Widget verlangt, und liest die fälligen Datenpunkte neu; unter iOS fordert die Timeline des
Widgets das nächste Neuladen in diesem Abstand an. 15 Minuten sind das Minimum der Plattform,
und beide Systeme behandeln den Wert als Ziel, nicht als Zusage — Android verschiebt ihn im
Doze-Modus, iOS plant innerhalb seines eigenen Budgets. Sinnvoll, wenn kein Push verfügbar ist
oder sich ein Wert still und selten ändert.

**4. Tippen — der Wert wird vor dem Ändern neu gelesen.**
Ein Toggle kehrt nicht einfach um, was auf der Kachel steht: Eine Kachel kann eine Stunde lang
auf dem Startbildschirm gelegen haben, und das Umkehren eines veralteten Werts schaltet in die
falsche Richtung. Deshalb liest das Tippen zuerst den aktuellen Wert, kehrt diesen um und
schreibt das Ergebnis. Eine *Wert setzen*-Kachel überspringt das Lesen, weil sie immer
denselben Wert schreibt.

Nach einem erfolgreichen Schreiben springt die Kachel **optimistisch** sofort auf den gerade
gesendeten Wert, markiert als „Befehl unterwegs“ (`ack = false`). Die Bestätigung des Adapters
(`ack = true`) kommt dann per Push und ersetzt sie. Erreicht das Schreiben den Datenpunkt
nicht, fällt die Kachel bei der nächsten Aktualisierung auf den echten Wert zurück.

```
 Datenpunkt ändert sich in ioBroker ──Push──► Kachel neu gezeichnet   (~1 s, braucht ioBroker.pro)
 Launcher zeichnet die Kachel neu ───────────► lesen, wenn älter als 60 s
 Timer der Auto-Aktualisierung ──────────────► lesen alle 15 / 30 / 60 min  (optional)
 du tippst auf die Kachel ───────────────────► lesen ─► umkehren ─► schreiben ─► optimistisch umspringen
```

---

## Was eingerichtet werden muss

### 1. In ioBroker — der web-Adapter

Die Widgets lesen und schreiben über den **`web`-Adapter**, dieselbe Instanz, die auch deine
Visualisierung ausliefert. Zwei seiner Optionen müssen aktiv bleiben, weil genau sie von den
Widgets benutzt werden:

- der **States-Endpunkt** (`/state/…`) — ohne ihn kann eine Kachel weder lesen noch schreiben
  und bleibt leer;
- der **Objects-Endpunkt** (`/objects`) — ohne ihn zeigt der Objektbrowser in der
  Widget-Konfiguration nichts an und du kannst keinen Datenpunkt auswählen.

In den Instanzeinstellungen deiner web-Instanz tauchen sie als Optionen zum *Deaktivieren* von
States und Objects auf (`disableStates` / `disableObjects`). Beide sind **standardmäßig aus**,
eine normale Installation funktioniert also bereits; ändere sie nur, falls jemand sie
eingeschaltet hat.

Der Standardport ist **8082** (`lovelace` nutzt **8091**).

### 2. In ioBroker — Benutzer und Rechte

Verlangt deine web-Instanz eine Anmeldung, dann braucht der Benutzer, den du im Tab **Lokal**
der App einträgst:

- **Leserecht** auf jeden Datenpunkt, den du anzeigen willst, und
- **Schreibrecht** auf jeden Datenpunkt, den du schalten willst.

Eine Kachel, die dauerhaft „unbekannt“ zeigt, oder ein Tippen, das fehlschlägt, obwohl der
Datenpunkt existiert, ist fast immer ein Rechteproblem und kein Fehler der App.

### 3. In ioBroker — ioBroker.pro für Push

Sofortige Aktualisierungen laufen über die ioBroker-Cloud. Dafür brauchst du:

- ein **ioBroker.pro**-Konto mit gültigem Abonnement,
- Cloud-Typ **Pro** im Cloud-Tab der App, mit eingetragenem Benutzernamen und Passwort.

Die App prüft das Konto und abonniert danach ein Benachrichtigungs-Thema, das aus deinem
Pro-Benutzernamen abgeleitet wird. Ohne gültigen Pro-Login gibt es keinen Push — die Widgets
funktionieren weiterhin, aktualisieren sich dann aber nur beim Neuzeichnen, bei der
automatischen Aktualisierung und beim Tippen. Wenn die Cloud nicht in Frage kommt, stelle bei
den wichtigen Kacheln ein Aktualisierungsintervall ein.

### 4. In der App

Richte mindestens das Projekt `default` so ein, dass die Verbindung funktioniert:

- Tab **Lokal**: `IP:PORT` der web-Instanz, dazu Benutzername und Passwort, falls nötig.
- Tab **Cloud** (unter iOS *Pro Cloud*): deine ioBroker.pro-Zugangsdaten, wenn du Push und Fernzugriff willst.

Teste es, indem du deine Visualisierung einmal in der App öffnest. Klappt das, haben die
Widgets alles, was sie brauchen.

### 5. Auf dem Gerät

**Android**

1. Lange auf eine freie Stelle des Startbildschirms drücken → **Widgets** → *ioBroker Visu*.
2. **ioBroker Toggle** oder **ioBroker Value** auf den Startbildschirm ziehen.
3. Der Konfigurationsbildschirm öffnet sich: Datenpunkt im Objektbrowser auswählen, dann
   Beschriftung, Icon, Farben, Bestätigung und Aktualisierungsintervall festlegen.
4. Kachel in der Größe ziehen — die Darstellung passt sich an.

Kommt die 15-Minuten-Aktualisierung zu spät oder gar nicht, nimm die App von der
Akkuoptimierung aus. Der Tab *Andere* in den Einstellungen bietet eine Abkürzung zu dieser
Systemeinstellung.

**iOS / iPadOS**

1. Lange auf den Startbildschirm drücken → **+** → *ioBroker Visu*.
2. Das **Übersichts**-Widget wählen (zeigt die ersten konfigurierten Kacheln, läuft auf jedem
   unterstützten System) oder das **Einzel**-Widget (eine ausgewählte Kachel; braucht
   **iOS 17**, weil es die AppIntent-Konfiguration nutzt).
3. Die Kacheln selbst werden in der App konfiguriert, in der Widget-Verwaltung.

Ab **iOS 17** schreibt ein Tippen direkt vom Startbildschirm aus. Unter **iOS 16** öffnet das
Tippen die App, die dann schreibt — das Ergebnis ist dasselbe, es dauert nur einen Moment
länger. Eine Analog-Kachel öffnet für ihren Schieberegler immer die App.

---

## Problembehebung

| Symptom | Ursache / Abhilfe |
|---|---|
| Kachel bleibt leer oder zeigt keinen Wert | Der Datenpunkt ist nicht lesbar: falsche IP/Port, falsche Zugangsdaten, kein Leserecht, oder der States-Endpunkt des web-Adapters ist deaktiviert |
| Objektbrowser ist leer | Der Objects-Endpunkt des web-Adapters ist deaktiviert, oder der Benutzer darf den Objektbaum nicht lesen |
| Wert aktualisiert sich nur beim Tippen | Kein Push — ioBroker.pro-Zugangsdaten fehlen oder sind ungültig. Als Behelf ein Aktualisierungsintervall einstellen |
| Tippen bewirkt nichts / meldet Fehler | Der Datenpunkt ist nicht beschreibbar (`common.write: false`), oder dem Benutzer fehlt das Schreibrecht |
| Kachel springt nach kurzer Zeit zurück | Das Schreiben kam nicht an oder der Adapter hat den Wert verworfen — die Kachel zeigt wieder den echten Zustand |
| Toggle schaltet in die falsche Richtung | Der Datenpunkt stellt An/Aus ungewöhnlich dar; `common.type`, `common.min`/`max` und `common.states` des Objekts prüfen |
| Tacho- oder Balkendarstellung fehlt | Der Datenpunkt hat weder die Einheit `%` noch einen Min/Max-Bereich, es gibt also keine Skala |
| Auto-Aktualisierung kommt zu spät (Android) | Doze-Modus — App von der Akkuoptimierung ausnehmen |
| Auto-Aktualisierung ist unregelmäßig (iOS) | Normal: iOS plant das Neuladen von Widgets in seinem eigenen Budget |
| Kachel funktioniert zu Hause, nicht unterwegs | Für dieses Projekt ist keine Cloud eingerichtet, der Fallback hat kein Ziel |
| Widget zeigt die falsche Installation | Die Kachel gehört zu einem anderen Projekt — neu konfigurieren und das richtige wählen |

---

## Widget-Fehler melden

[Ein Issue anlegen](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) und
zusätzlich zu Gerät und App-Version angeben:

- den **Widget-Typ** (Toggle oder Analog), bei Analog zusätzlich die Darstellungsart,
- die **Datenpunkt-ID** und ihre `common`-Definition (type, role, min, max, unit, write,
  states),
- ob die Kachel **lokal oder über die Cloud** verbunden ist,
- ob **Push** funktioniert (ändert sich der Wert von selbst, wenn du den Datenpunkt anderswo
  schaltest?),
- das eingestellte **Aktualisierungsintervall**.
