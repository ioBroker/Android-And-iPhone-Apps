<img src="docs/images/app-icon.png" width="96" align="right" alt="ioBroker Visu App-Icon" />

# ioBroker Android- und iPhone-Apps

**Issue-Tracker und Informationsseite für die offiziellen ioBroker-Apps.**

Dieses Repository enthält **nicht** den Quellcode der Apps. Es existiert, damit alle
Fehlermeldungen, Feature-Wünsche und Informationen zu den ioBroker-Apps für Android, iPhone
und iPad an einer Stelle innerhalb der ioBroker-Organisation gesammelt werden.

👉 **[Fehler melden oder Feature vorschlagen](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose)**

🇬🇧 [English version of this page](README.md)

---

## Die Apps

| App | Plattform | Store | Dokumentation |
|---|---|---|---|
| **ioBroker Visu** | Android Smartphone & Tablet | [Google Play](https://play.google.com/store/apps/details?id=com.iobroker.visu) | [docs/android.de.md](docs/android.de.md) |
| **ioBroker Visu** | iPhone & iPad | [App Store](https://apps.apple.com/app/iobroker-visu/id1673095774) | [docs/ios.de.md](docs/ios.de.md) |

Beide Apps werden von der **ioBroker GmbH** herausgegeben, sind **kostenlos** und enthalten
weder Werbung noch In-App-Käufe. Sie teilen sich ein Einstellungsmodell — eine für die eine
Plattform beschriebene Option bedeutet auf der anderen dasselbe.

### Was die Apps machen

Die Apps sind ein auf den Zweck zugeschnittener Vollbild-Container für die Visualisierung,
die ohnehin schon auf deiner ioBroker-Installation läuft — `vis-2`, `vis`, `lovelace`,
`material`, `jarvis`, `iQontrol`, `habpanel` oder `devices`. Statt diese Seite im mobilen
Browser zu öffnen, bekommst du:

- eine gespeicherte Verbindungskonfiguration, lokal **und** von außen, mit automatischem
  Umschalten zwischen Heimnetz und **ioBroker.pro**-Cloud anhand der WLAN-SSID;
- **Homescreen-Widgets**, die einen Datenpunkt schalten oder einen Wert anzeigen, ohne die App
  zu öffnen — siehe **[docs/widgets.de.md](docs/widgets.de.md)** zum Aktualisierungsprinzip
  und zur Einrichtung;
- **Push-Benachrichtigungen** aus ioBroker, mit Titel, Priorität, Ablaufzeit, Aktionsknöpfen
  und gezielter Zustellung an einzelne Geräte;
- Gerätedaten zurück nach ioBroker: Akku, Bildschirmhelligkeit, Standort, WLAN-SSID,
  Verbindungsart und eine Online-Anzeige je Gerät;
- **Matter**-Inbetriebnahme über den ioBroker-Matter-Adapter;
- **Geofence**-Anwesenheitserkennung;
- Wandpanel-Verhalten: Display wachhalten, nach Inaktivität dimmen, Ausrichtung sperren,
  Status- und Navigationsleiste ausblenden, nach Inaktivität zur Startseite zurückkehren;
- biometrischen Schutz für App-Start und Einstellungen;
- bis zu **3 Projekte** (Verbindungsprofile), jedes über eine eigene Verknüpfung erreichbar.

Die vollständige Funktionsliste je Plattform steht in der oben verlinkten Dokumentation.

---

## Dokumentation

| Seite | Inhalt |
|---|---|
| [docs/android.de.md](docs/android.de.md) | Android-App: Store-Link, Screenshots, vollständige Funktions- und Einstellungsreferenz |
| [docs/ios.de.md](docs/ios.de.md) | iPhone-/iPad-App: Store-Link, Screenshots, vollständige Funktions- und Einstellungsreferenz |
| [docs/widgets.de.md](docs/widgets.de.md) | Homescreen-Widgets: Aktualisierungsprinzip und was dafür eingerichtet werden muss |

---

## Issue anlegen

1. **Zuerst die [vorhandenen Issues](https://github.com/ioBroker/Android-And-iPhone-Apps/issues?q=is%3Aissue) durchsuchen** — das Problem ist womöglich schon gemeldet.
2. Ein [neues Issue](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) anlegen und **🐞 Bug** oder **🌟 Feature request** wählen.
3. Immer angeben:
   - **Plattform**: Android oder iOS
   - **Betriebssystem-Version**: z. B. `Android 15` / `iOS 18.5`
   - **Gerät**: z. B. `Pixel 8` / `iPhone 14 Pro`
   - **App-Version**: steht unten auf dem Einstellungsbildschirm
   - **Verwendete Visualisierung**: `vis-2`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`, …
   - **Verbindung**: lokal, ioBroker.pro-Cloud oder eigene Cloud
   - Schritte zum Nachstellen, möglichst mit Screenshot oder Bildschirmaufnahme

> ⚠️ Bitte IP-Adressen, Benutzernamen, Passwörter und ioBroker.pro-Zugangsdaten in
> Screenshots und Logs unkenntlich machen, bevor du sie hochlädst.

### Was hierher gehört — und was nicht

| Thema | Richtige Stelle |
|---|---|
| App stürzt ab, weiße Seite, Einstellungen werden nicht gespeichert, Gesten, Statusleiste, Zoom, Widgets, Push, Matter, Geofence | **Dieses Repository** |
| Ein Widget *der Visualisierung* wird auch im Desktop-Browser falsch dargestellt | [ioBroker.vis-2](https://github.com/ioBroker/ioBroker.vis-2) / [ioBroker.vis](https://github.com/ioBroker/ioBroker.vis) |
| Probleme mit `jarvis`, `iQontrol`, `lovelace`, `material`, `habpanel` | Repository des jeweiligen Adapters |
| Endpunkt `/state/` oder `/objects` fehlt oder verweigert den Zugriff | [ioBroker.web](https://github.com/ioBroker/ioBroker.web) |
| Cloud-Konto, Abrechnung, ioBroker.pro-Login | [ioBroker.pro](https://iobroker.pro)-Support |
| „Wie baue ich diese View?“, allgemeine Anwendungsfragen | [ioBroker-Forum](https://forum.iobroker.net/) |

**Faustregel:** Tritt dasselbe Problem auch auf, wenn du die Visualisierung in einem normalen
mobilen Browser öffnest, dann ist es kein App-Problem.

> Begriffsklärung: *Widget* bedeutet zweierlei. Ein **vis-Widget** ist ein Element innerhalb
> deiner Visualisierung und gehört in die vis-Repositories. Ein **Homescreen-Widget** ist eine
> Kachel auf dem Startbildschirm des Telefons und gehört hierher — siehe
> [docs/widgets.de.md](docs/widgets.de.md).

---

## Links

- 💬 [ioBroker-Forum](https://forum.iobroker.net/) — Fragen und Community-Hilfe
- 📣 [Forums-Thread zur App](https://forum.iobroker.net/topic/63321/) — Ankündigungen und Diskussion
- ☁️ [ioBroker.pro](https://iobroker.pro) — Cloud für Fernzugriff und Push
- 📚 [ioBroker-Dokumentation](https://www.iobroker.net/#de/documentation)

### Vorgänger-Repository

Issues zur ioBroker-Visu-App wurden früher unter
[foxriver76/ioBroker-Visu-App](https://github.com/foxriver76/ioBroker-Visu-App) geführt.
Ältere Meldungen sind dort weiterhin lesbar — **neue Issues gehören hierher.**

---

Die Screenshots in [`docs/images`](docs/images) sind die offiziellen Store-Screenshots der
ioBroker-Visu-App, veröffentlicht von der ioBroker GmbH.
