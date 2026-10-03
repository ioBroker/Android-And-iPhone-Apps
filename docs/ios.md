<img src="images/app-icon.png" width="88" align="right" alt="ioBroker Visu app icon" />

# ioBroker Visu — iPhone & iPad

[⬅️ Back to the overview](../README.md) · 🇩🇪 [Deutsche Version](ios.de.md)

**📲 [Install from the App Store](https://apps.apple.com/app/iobroker-visu/id1673095774)**

| | |
|---|---|
| **App name** | ioBroker Visu |
| **Bundle id** | `com.iobroker.visu` |
| **Seller** | ioBroker GmbH |
| **Price** | Free — no ads, no in-app purchases |
| **Category** | Lifestyle |
| **Requires** | iOS / iPadOS 16.1 or later |
| **Devices** | iPhone, iPad, Mac with Apple silicon |
| **Languages** | English, German, Russian |
| **Store link** | <https://apps.apple.com/app/iobroker-visu/id1673095774> |

> There is an older app simply called **ioBroker**
> ([id1449564305](https://apps.apple.com/app/iobroker/id1449564305)) in the App Store. It is
> the predecessor and is no longer developed. Please install **ioBroker Visu**.

---

## Screenshots

| Your visualization | Connection settings |
|---|---|
| <img src="images/ios/vis-dashboard-iphone.png" width="250" alt="vis dashboard on an iPhone" /> | <img src="images/ios/settings-connection-iphone.png" width="250" alt="Connection settings on an iPhone" /> |

On the iPad the same views use the full width:

| Dashboard | Navigation drawer | Full settings list |
|---|---|---|
| <img src="images/ios/vis-dashboard-ipad.png" width="260" alt="Dashboard on an iPad" /> | <img src="images/ios/vis-menu-ipad.png" width="260" alt="Navigation drawer on an iPad" /> | <img src="images/ios/settings-full-ipad.png" width="260" alt="Complete settings list on an iPad" /> |

*These are the current App Store screenshots. The app is developed continuously, so the
settings screen in the latest release may be grouped differently than shown here — the
reference below describes the current structure.*

---

## What the app does

The app renders the visualization that already runs on your ioBroker installation inside a
tuned full-screen `WKWebView`, and adds the things Safari cannot do: a saved connection,
automatic local/remote switching, home-screen widgets, push notifications, device sensors,
Matter commissioning and kiosk behaviour.

The iOS app and the Android app share one settings model, so every option means the same
thing on both — the differences are listed under [Differences from
Android](#differences-from-android).

### Supported visualizations

`vis-2` · `vis` · `lovelace` · `material` · `jarvis` · `iQontrol` · `habpanel` · `devices`

The chosen type only decides which URL the app opens, so anything else reachable on your web
instance can be used as well. The default port is **8082**, except for `lovelace`, which
defaults to **8091**.

### Connection

- **Local** — IP and port of your web instance, e.g. `192.168.1.10:8082`. A bare `IP:PORT`
  is completed automatically; `https://` may be given explicitly. An optional user name and
  password perform an automatic login.
- **Pro Cloud** — your [ioBroker.pro](https://iobroker.pro) account for access from outside.
  The subscription is validated against the cloud, and a Pro logo can be shown in the corner
  while the cloud connection is in use.
- **Custom cloud** — instead of ioBroker.pro, any self-hosted URL.
- **Wi-Fi SSIDs** — a comma-separated list of your home networks. While connected to one of
  them the app uses the local URL, otherwise the cloud.
- **QR code setup** — the Local tab has a scanner for the `iotConfig` code produced by
  ioBroker, which fills in port, IP, cloud user and password in one step.
- **Session recovery** — an expired session produces no error, only a redirect to a login
  page. The app renews the session cookie before it expires, renews again when it returns to
  the foreground, and recognises a login page by its URL to log in silently and return to the
  page you were on. This is what keeps a permanently mounted iPad logged in.

### Home-screen widgets

Two tile types — a **Toggle** that switches a state, and an **Analog** tile that shows a
numeric value as a number, half-circle gauge, horizontal or vertical bar. They come in two
flavours: an **overview** widget that shows the first configured tiles and works on every
supported system, and a **single** widget you point at one chosen tile, which needs iOS 17.

➡️ **[widgets.md](widgets.md) — how widgets update and what you have to configure.**

### Push notifications

Messages sent from ioBroker (`iot.0.app.message`, optionally with `app.title`, `app.expire`
and `app.priority`) arrive as iOS notifications with action buttons; the tapped action is
written back to ioBroker. A notification can target specific devices by name and can carry a
URL to open. Push requires a valid ioBroker.pro account.

### Device telemetry

The app can report back into ioBroker: **battery** level and charging state, **screen
brightness** (bidirectional — writing the state dims the device), **location**, **Wi-Fi
SSID**, **connection type**, a **device name** and an online indicator. Two destinations are
selectable: the `cloud` adapter (states appear under `cloud.X.devices.<device>`) or directly
under `vis.0.<device>.<field>`.

While the visualization is on screen the app reports on its own connection every 45 seconds.
Off screen, `BGTaskScheduler` runs a round roughly every 15 minutes — iOS decides the exact
moment, so the cadence is a target, not a guarantee. For a device that must report
continuously there is an opt-in mode that keeps the process alive through location updates;
it costs the "Always" location permission and the visible location indicator.

### Matter

The app ships an Apple `MatterSupport` device-setup extension. Scanning a device's QR code
hands the commissioning over to the ioBroker matter adapter, which adds the device to your
installation.

### Geofence

Named locations with a radius (minimum 100 m); entering or leaving one writes a boolean state
under `iot.0.app.geofence.<name>`, which the adapter creates on first use.

### Kiosk / wall-panel behaviour

Keep the display awake · dim to a chosen level after N seconds of inactivity and restore on
the next tap · return to the start page after N seconds · lock the orientation · show, hide
or make transparent the status bar (with a free colour) · force full screen · fixed or
automatic zoom, separately for portrait and landscape · allow or block scrolling and zooming.

### Projects

Up to **3 projects**, each with its own connection, visualization and appearance. A long
press on the app icon offers one Quick Action per project; starting the app through a Quick
Action locks it to that project until it is restarted.

### Protection

Face ID / Touch ID can be required for the app start and for opening the settings,
independently of each other.

---

## Settings reference

The settings screen opens with a **three-finger tap** on the visualization, and is organised
in five tabs.

### Local

| Setting | Meaning |
|---|---|
| Host IP:PORT | Address of the web instance, e.g. `192.168.1.10:8082`. `https://` allowed |
| User name / Password | ioBroker user for the automatic login |
| QR scanner | Reads an `iotConfig` code and fills in the fields |

### Pro Cloud

| Setting | Meaning |
|---|---|
| Cloud type | `Pro` (iobroker.pro) or `Custom` |
| Cloud URL | Only for `Custom` |
| User name / Password | ioBroker.pro account — also enables push notifications |
| Wi-Fi SSIDs | Comma-separated home networks; inside them the local URL is used |

### Application

| Setting | Meaning |
|---|---|
| Application | `vis-2`, `vis`, `lovelace`, `material`, `jarvis`, `iQontrol`, `habpanel`, `devices` |
| Project | vis project name, default `main` |
| URL postfix | Appended to the URL, e.g. `#myStartView` |
| Instance ID | Identifies this device for `vis.0.control` (switch views, detect the active view) |

### Others

| Setting | Meaning |
|---|---|
| Allow zoom / Allow scrolling | Enable or block the gestures in the WebView |
| Zoom (portrait) / Zoom (landscape) | Fixed initial scale per orientation |
| Automatic zoom | Sets `width=device-width`, so the page scales itself |
| Force full screen | Sets `viewport-fit=cover` |
| Reload on orientation change | Helps with views that do not re-layout cleanly |
| Orientation | Lock to portrait or landscape |
| Status bar | Shown, hidden or transparent, with a free colour and light text |
| Keep display awake | Prevents the screen from turning off |
| Dim after seconds / Dim to level | Dim after inactivity, restore on the next tap (`0` = off) |
| Back to start page after seconds | Return to the start view after inactivity (`0` = off) |
| Reload when the app becomes active | Hard reload when returning from the background (on by default on iOS) |
| Telemetry target | `cloud` adapter or `vis.0` |
| Battery / Location / Brightness / Device name | Which values are reported |
| Report permanently in the background | Keeps reporting alive through location updates; needs the "Always" permission |
| Device name | Name used for the states of this device |
| Show Pro logo | Indicator in the corner while the cloud connection is in use |
| Protect app start / Protect settings | Face ID / Touch ID lock |
| Language / Dark mode | App language (EN/DE/RU) and theme |

### Matter

Selection of the matter instance and the commissioning dialog.

---

## Gestures

| Gesture | Effect |
|---|---|
| Three-finger tap | Open the settings |
| Pull to refresh | Reload the page — only when the page is already scrolled to the top |
| Tap after dimming | Restore the previous brightness |
| Long press on the app icon | Start a specific project (Quick Action) |

---

## Differences from Android

| Topic | iOS |
|---|---|
| Interactive widgets | Writing from the tile itself needs iOS 17. On iOS 16 a tap opens the app, which performs the write |
| Reload gesture | Pull to refresh instead of the two-finger double tap |
| Navigation bar | Android-only — iOS has no counterpart |
| Background reporting | `BGTaskScheduler`; iOS decides the cadence, so a round is not guaranteed every 15 minutes |
| Matter | Apple's `MatterSupport` extension instead of Google Play Services |
| VPN detection | Not available — iOS does not let an app read or control the VPN state |

---

## Troubleshooting

| Symptom | Cause / remedy |
|---|---|
| Settings open on every start | The connection test failed — check IP, port, credentials and whether the web instance is running |
| Blank page | Wrong application type or wrong project name; check the port (8082, lovelace 8091) |
| Works at home, not outside | No cloud configured, or the Wi-Fi SSID list is missing, so the app keeps trying the local address |
| Keeps returning to the login page | Credentials wrong, or the user lacks permission for the view |
| Pull to refresh does not trigger | By design — it only works when the page is already at the top, so that reading up a long view does not reload it |
| Widget tile stays empty | See [widgets.md](widgets.md) — usually the `/state/` endpoint of the web adapter |
| Single-tile widget not offered | It needs iOS 17; on iOS 16 use the overview widget |
| No push notifications | ioBroker.pro credentials missing or invalid; push is tied to a valid Pro account |
| Background values arrive irregularly | Expected on iOS — the system schedules the background rounds |

---

## Reporting a bug

[Open an issue](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) and
include the iOS version, the device model, the app version (bottom of the settings screen),
the visualization used and the connection type. Redact IP addresses, user names and passwords
in screenshots.
