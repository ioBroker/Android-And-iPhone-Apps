# Home-screen widgets

[⬅️ Back to the overview](../README.md) · 🇩🇪 [Deutsche Version](widgets.de.md)

A home-screen widget is a tile on the phone's or tablet's home screen that shows one ioBroker
state and — if the state is writable — changes it, **without opening the app**.

> *Widget* means two different things in the ioBroker world. A **vis widget** is an element
> inside your visualization. This page is about the **home-screen widget** of the mobile
> operating system. The two have nothing to do with each other.

---

## The two tile types

| | Toggle | Analog |
|---|---|---|
| **Purpose** | Switch a state on/off, or write one fixed value | Show a numeric value |
| **Typical states** | `switch`, `button`, booleans | temperature, power, battery, humidity |
| **Display** | Icon, label, active/inactive colour | Number with unit, half-circle gauge, horizontal bar, vertical bar |
| **Tap** | Writes immediately — optionally after a confirmation dialog | Writable state: slider dialog. Read-only state: refreshes the value |

Both are size-adaptive — icon, label, value and gauge scale with the size you resize the tile
to — and can be reconfigured after placement. The gauge and bar styles are only offered when
the state carries a `%` unit or has both `common.min` and `common.max`, because a bar without
a range has nothing to fill.

---

## How a widget gets its value — the update principle

A widget is a separate process from the app. It does **not** use the WebView and it does
**not** use the vis socket — the visualization does not even have to be open. Instead the
widget talks plain REST to your ioBroker installation:

| Purpose | Request |
|---|---|
| Read a state | `GET {base}/state/{id}` |
| Write a state | `POST {base}/state/{id}` with body `{"val": …}` |
| Browse the object tree | `GET {base}/objects?pattern=…` |

`{base}` is resolved **local first, cloud second**: the widget tries the project's local URL
with a 3-second timeout, and only if that fails does it fall back to the project's cloud
(`https://iobroker.pro` or your custom URL) with a 5-second timeout. That is why the same
tile works at home and on mobile data. Credentials go along as HTTP Basic auth — the local
ones for the local attempt, the Pro ones for the cloud attempt.

Each widget remembers which **project** it belongs to, so a tile always uses that project's
URL and credentials.

### The four things that refresh a tile

**1. Push — instant, the normal case.**
The ioBroker cloud sends a message carrying `id`, `value` and `ack`. The app receives it even
while it is in the background or closed, stores the value for **every** widget whose state id
matches, and forces the tile to redraw. This is what makes a lamp tile flip within a second
of someone switching the lamp by any other means. Push needs a valid **ioBroker.pro** account
— see the prerequisites below.

**2. Redraw — the 60-second safety net (Android).**
Whenever the launcher asks the tile to redraw, the widget checks how old its cached value is.
If there is no value yet, or the cached one is older than 60 seconds, it reads the state again
before drawing. So a tile that comes back into view is never stale by more than a minute.

**3. Auto-refresh — polling, off by default.**
Each widget can be set to **off (push only) / every 15 minutes / every 30 minutes / every
hour**. On Android a single WorkManager job runs at the shortest interval any widget asked
for and re-reads the states that are due; on iOS the widget's timeline requests the next
reload at that interval. 15 minutes is the platform minimum, and both platforms treat it as a
target rather than a promise — Android defers it in doze mode, iOS schedules it inside its own
budget. Turn this on when push is not available or when a value changes silently and rarely.

**4. Tap — the value is re-read before it is changed.**
A Toggle does not simply invert what is painted on the tile: a tile may have been sitting on
the home screen for an hour, and inverting a stale value switches the wrong way. So the tap
first reads the live value, inverts that, and writes the result. A *Set value* tile skips the
read, since it always writes the same value.

After a successful write the tile flips **optimistically** — immediately to the value just
sent, marked as "command in flight" (`ack = false`). The adapter's confirmation
(`ack = true`) then arrives by push and replaces it. If the write never reaches a state, the
tile falls back to the real value on its next refresh.

```
 state changes in ioBroker ──push──► tile redraws          (~1 s, needs ioBroker.pro)
 launcher redraws the tile ─────────► read if older than 60 s
 auto-refresh timer ────────────────► read every 15 / 30 / 60 min  (optional)
 you tap the tile ──────────────────► read ─► invert ─► write ─► flip optimistically
```

---

## What you have to set up

### 1. In ioBroker — the web adapter

The widgets read and write through the **`web` adapter**, the same instance that serves your
visualization. Two of its options must stay enabled, because both are what the widgets use:

- the **states endpoint** (`/state/…`) — without it a tile can neither read nor write and
  stays empty;
- the **objects endpoint** (`/objects`) — without it the object browser in the widget
  configuration shows nothing and you cannot pick a state.

In the instance settings of your web instance these appear as the options to *disable* states
and objects (`disableStates` / `disableObjects`). Both are **off by default**, so a standard
installation already works; only change them if someone switched them on.

The default port is **8082** (`lovelace` uses **8091**).

### 2. In ioBroker — the user and permissions

If your web instance requires authentication, the user you enter in the app's **Local** tab
must have:

- **read** permission on every state you want to display, and
- **write** permission on every state you want to switch.

A tile that only ever shows "unknown", or a tap that reports a failure although the state
exists, is almost always a permission problem rather than a bug.

### 3. In ioBroker — ioBroker.pro, for push

Instant updates arrive over the ioBroker cloud. For them you need:

- an **ioBroker.pro** account with a valid subscription,
- cloud type **Pro** in the app's cloud tab, with user name and password entered.

The app verifies the account and then subscribes to a notification topic derived from your
Pro user name. Without a valid Pro login there is no push — the widgets still work, but they
only update on redraw, on auto-refresh and on tap. If you cannot use the cloud, set an
auto-refresh interval on the tiles that matter.

### 4. In the app

Configure at least the `default` project so that the connection works:

- **Local** tab: host `IP:PORT` of the web instance, plus user name and password if required.
- **Cloud** tab (*Pro Cloud* on iOS): your ioBroker.pro credentials, if you want push and remote access.

Test it by opening your visualization in the app once. If that works, the widgets have
everything they need.

### 5. On the device

**Android**

1. Long-press an empty spot on the home screen → **Widgets** → *ioBroker Visu*.
2. Drag **ioBroker Toggle** or **ioBroker Value** onto the home screen.
3. The configuration screen opens: pick the state in the object browser, then set label,
   icon, colours, confirmation and auto-refresh.
4. Resize the tile — the layout adapts.

If the 15-minute auto-refresh arrives late or not at all, exclude the app from battery
optimisation. The *Others* tab in the settings has a shortcut to that system setting.

**iOS / iPadOS**

1. Long-press the home screen → **+** → *ioBroker Visu*.
2. Choose the **overview** widget (shows the first configured tiles, works on every supported
   system) or the **single** widget (one chosen tile; needs **iOS 17**, because it uses
   AppIntent configuration).
3. Configure the tiles themselves inside the app, under the widget management screen.

On **iOS 17 and later** a tap writes directly from the home screen. On **iOS 16** the tap
opens the app, which performs the write — the result is the same, it just takes a moment
longer. An analog tile always opens the app for its slider.

---

## Troubleshooting

| Symptom | Cause / remedy |
|---|---|
| Tile stays empty or shows no value | The state cannot be read: wrong IP/port, wrong credentials, no read permission, or the states endpoint of the web adapter is disabled |
| Object browser is empty | The objects endpoint of the web adapter is disabled, or the user may not read the object tree |
| Value only updates when I tap | No push — ioBroker.pro credentials missing or invalid. Set an auto-refresh interval as a workaround |
| Tap does nothing / reports a failure | The state is not writable (`common.write: false`), or the user lacks write permission |
| Tile switches back after a moment | The write did not arrive, or the adapter rejected the value — the tile returns to the real state |
| Toggle switches the wrong way | The state has a non-standard on/off representation; check `common.type`, `common.min`/`max` and `common.states` of the object |
| Gauge or bar style not offered | The state has no `%` unit and no min/max range, so there is nothing to scale against |
| Auto-refresh is late (Android) | Doze mode — exclude the app from battery optimisation |
| Auto-refresh is irregular (iOS) | Expected: iOS schedules widget reloads inside its own budget |
| Tile works at home but not outside | No cloud configured for that project, so the fallback has nowhere to go |
| Widget shows the wrong installation | The tile belongs to a different project — reconfigure it and pick the right one |

---

## Reporting a widget bug

[Open an issue](https://github.com/ioBroker/Android-And-iPhone-Apps/issues/new/choose) and
include, in addition to the usual device and app version:

- the **widget type** (Toggle or Analog) and, for Analog, the display style,
- the **state ID** and its `common` definition (type, role, min, max, unit, write, states),
- whether the tile is connected **locally or through the cloud**,
- whether **push** works (does the value change on its own when you switch the state
  elsewhere?),
- the configured **auto-refresh interval**.
