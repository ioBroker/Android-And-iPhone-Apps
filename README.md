<img src="docs/images/app-icon.png" width="96" align="right" alt="ioBroker Visu app icon" />

# ioBroker Android & iPhone Apps

**Issue tracker and information hub for the official ioBroker mobile apps.**

This repository does **not** contain the source code of the apps. It exists so that all bug
reports, feature requests and information about the ioBroker apps for Android, iPhone and
iPad are collected in one place inside the ioBroker organisation.

👉 **[Report a bug or request a feature](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose)**

🇩🇪 [Deutsche Version dieser Seite](README.de.md)

---

## The apps

| App | Platform | Store | Documentation |
|---|---|---|---|
| **ioBroker Visu** | Android phone & tablet | [Google Play](https://play.google.com/store/apps/details?id=com.iobroker.visu) | [docs/android.md](docs/android.md) |
| **ioBroker Visu** | iPhone & iPad | [App Store](https://apps.apple.com/app/iobroker-visu/id1673095774) | [docs/ios.md](docs/ios.md) |

Both apps are published by **ioBroker GmbH**, are **free of charge** and contain no ads and
no in-app purchases. They share one configuration model, so a setting described for one
platform means the same thing on the other.

### What the apps do

The apps are a tuned, full-screen container for the visualization that already runs on your
ioBroker installation — `vis-2`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`,
`habpanel` or `devices`. Instead of opening that page in a mobile browser you get:

- a saved connection configuration, local **and** remote, with automatic switching between
  the home network and the **ioBroker.pro** cloud based on the current Wi-Fi SSID;
- **home-screen widgets** that switch a state or show a value without opening the app —
  see **[docs/widgets.md](docs/widgets.md)** for how they update and what has to be set up;
- **push notifications** from ioBroker, with title, priority, expiry, action buttons and
  per-device targeting;
- device telemetry back into ioBroker: battery, screen brightness, location, Wi-Fi SSID,
  connection type and an online indicator per device;
- **Matter** commissioning through the ioBroker matter adapter;
- **geofence** presence detection;
- wall-panel behaviour: keep the display awake, dim after inactivity, lock the orientation,
  hide the status and navigation bars, return to the start page after inactivity;
- biometric protection of app start and of the settings screen;
- up to **3 projects** (connection profiles), each reachable from its own home-screen
  shortcut.

The complete, per-platform feature list is in the documentation linked above.

---

## Documentation

| Page | Content |
|---|---|
| [docs/android.md](docs/android.md) | Android app: store link, screenshots, full feature and settings reference |
| [docs/ios.md](docs/ios.md) | iPhone/iPad app: store link, screenshots, full feature and settings reference |
| [docs/widgets.md](docs/widgets.md) | Home-screen widgets: how they update and what you must configure |

German versions: [android.de.md](docs/android.de.md) · [ios.de.md](docs/ios.de.md) · [widgets.de.md](docs/widgets.de.md)

---

## Reporting an issue

1. **Search the [existing issues](https://github.com/ioBroker/Android-And-iPhone-Apps/issues?q=is%3Aissue)** first — your problem may already be reported.
2. Open a [new issue](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) and pick **🐞 Bug** or **🌟 Feature request**.
3. Always include:
   - **Platform**: Android or iOS
   - **OS version**: e.g. `Android 15` / `iOS 18.5`
   - **Device**: e.g. `Pixel 8` / `iPhone 14 Pro`
   - **App version**: shown at the bottom of the settings screen in the app
   - **Visualization** used: `vis-2`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`, …
   - **Connection**: local, ioBroker.pro cloud or custom cloud
   - Steps to reproduce, plus a screenshot or screen recording if possible

> ⚠️ Please redact IP addresses, user names, passwords and ioBroker.pro credentials from
> screenshots and logs before uploading them.

### What belongs here — and what does not

| Topic | Where it belongs |
|---|---|
| App crashes, blank screen, settings not saved, gestures, status bar, zoom, widgets, push, Matter, geofence | **This repository** |
| A widget of the *visualization* renders wrong in the desktop browser too | [ioBroker.vis-2](https://github.com/ioBroker/ioBroker.vis-2) / [ioBroker.vis](https://github.com/ioBroker/ioBroker.vis) |
| Problems with `jarvis`, `iQontrol`, `lovelace`, `material`, `habpanel` | The repository of that adapter |
| `/state/` or `/objects` endpoint missing or refusing access | [ioBroker.web](https://github.com/ioBroker/ioBroker.web) |
| Cloud account, billing, ioBroker.pro login | [ioBroker.pro](https://iobroker.pro) support |
| "How do I build this view?", general usage questions | [ioBroker Forum](https://forum.iobroker.net/) |

**Rule of thumb:** if the same problem also happens when you open the visualization in a
normal mobile browser, it is not an app issue.

> Note on terminology: *widget* means two different things. A **vis widget** is an element
> inside your visualization and belongs to the vis repositories. A **home-screen widget** is
> a tile on the phone's home screen and belongs here — see [docs/widgets.md](docs/widgets.md).

---

## Links

- 💬 [ioBroker Forum](https://forum.iobroker.net/) — questions and community support
- 📣 [Forum thread of the app](https://forum.iobroker.net/topic/63321/) — announcements and discussion
- ☁️ [ioBroker.pro](https://iobroker.pro) — the cloud used for remote access and push
- 📚 [ioBroker documentation](https://www.iobroker.net/#en/documentation)

### Predecessor repository

Issues for the ioBroker Visu app were previously tracked in
[foxriver76/ioBroker-Visu-App](https://github.com/foxriver76/ioBroker-Visu-App). Older
reports can still be read there — **new issues belong here.**

---

The screenshots in [`docs/images`](docs/images) are the official store screenshots of the
ioBroker Visu app, published by ioBroker GmbH.
