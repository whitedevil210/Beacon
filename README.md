# Beacon

**Plan the day you can actually finish.**

Beacon is an offline Android task planner. It learns when you do your best work, tells you what won't fit in your day, and keeps every task on your phone. There are no accounts, no analytics, no ads, and the app doesn't request internet permission.

Built with Kotlin, Jetpack Compose and Room.

## Features

**Planning**
- **Energy-aware planner.** Tasks are sorted as light, medium or deep work. Deep work goes to your sharpest hours, light admin to your dips.
- **Honest plans.** Anything that doesn't fit today is listed with a reason: too long for today, blocked, or out of time.
- **Slip forecasts.** Each task shows whether it's on track, worth watching or likely to slip, with the reasons.
- **Learns your pace.** Beacon learns how long things take you and how much you get done on a normal day.
- **Calendar-aware (optional).** "Plan around my calendar" skips your busy hours. Only event times are read.

**Capture**
- **Quick add** in plain words: `Gym every monday at 7am p2 #health`. A live preview shows what was understood.
- **Voice input** and **Share to Beacon** from any app.
- **Search language:** `overdue`, `today`, `p1`, `deep work`, `done last week`, `@project`, `#tag`, and more. Beacon shows how it read your query.

**Staying on track**
- **Reminders** that fire at the exact minute, with Snooze and Complete actions. They are restored after a reboot.
- **Home-screen widget** with today's tasks, P1 and P2 priorities and your next alarm.
- **Floating panel (optional)** to capture tasks over other apps.
- **Focus timer** linked to a task, and **habit streaks**.

**Looking back**
- **Daily review.** Compare your plan with what happened, then roll unfinished tasks into tomorrow.
- **Analytics and insights.** Weekly completions, focus minutes, and insights that stay quiet until there is enough data.
- **Smart inbox.** Spots duplicates, stale tasks and tasks that are blocking others.

**Organising**
- Projects with deadlines, tags, categories, subtasks, dependencies and a kanban board.
- Priorities P1 (critical) to P5 (optional).

## Privacy and security

- No internet permission, no analytics, no ads.
- All data is stored locally in a Room database.
- Optional PIN and biometric lock. The PIN is hashed with PBKDF2 and a random salt, and repeated wrong attempts trigger an increasing lockout.
- Optional encrypted backups: PBKDF2-HMAC-SHA256 key derivation and AES-256-GCM. If you lose the passphrase, the backup can't be recovered.
- Backups don't include alarms, widget settings, app settings, your PIN or attachments. Re-create your reminders after restoring.

## Permissions

| Permission | Why |
|---|---|
| Notifications | Show reminders |
| Exact alarms | Fire reminders at the exact minute |
| Run at startup | Restore reminders after a reboot |
| Display over other apps (optional) | Floating quick panel |
| Calendar (optional) | Only when you tap "Plan around my calendar" |
| Biometrics | Unlock the app |
| Vibrate, wake lock | Reminder feedback |

## Requirements

- Android 8.0 (API 26) or newer
- Target SDK 34

## Install

Download the APK from the [latest release](../../releases/latest) and open it on your phone. Android will ask you to allow installs from that source.

## Build from source

You need Android Studio (Hedgehog 2023.1 or newer), Android SDK Platform 34 and JDK 17.

```bash
git clone https://github.com/whitedevil210/Beacon.git
cd Beacon
./gradlew :app:testDebugUnitTest
./gradlew assembleDebug
```

The debug APK is created at `app/build/outputs/apk/debug/app-debug.apk`. Install it with:

```bash
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

The debug build uses the application ID `com.beacon.beacon.debug`.

## Project structure

```
app/src/main/java/com/beacon/beacon/
├── alarms/          exact alarms, boot recovery
├── backup/          export, import, encryption
├── calendar/        optional calendar reader
├── data/            Room database, DAOs, repository
├── domain/          planner, energy, risk, review, search logic
├── notifications/   reminders, digest, review nudges
├── overlay/         floating quick panel
├── security/        PIN and lockout
├── ui/              Compose screens, components, theme
└── widget/          home-screen widget
```

The planning and search logic lives in `domain/` with no Android dependencies, so it is covered by plain JVM unit tests.

## Status

Current release: **v0.1**.

## Author

Made by [@whitedevil210](https://github.com/whitedevil210).
