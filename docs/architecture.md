# Architecture

ALO is built so that understanding your day never requires sending your day anywhere.

```text
Application signals
↓
Local event normalisation
↓
Session grouping
↓
Local storage
↓
Memory
↓
Optional AI
```

## Principles

**Signals, not content.** Collectors record which app, which project, how long and what kind of thing happened. They do not record screens, keystrokes, message bodies or document text.

**Normalise at the boundary.** Every signal becomes a small `alo/1` event with bounded fields. Anything that looks like content is refused before it is stored. Private Zones are checked here too, so a blocked event leaves no trace.

**Sessions, not timers.** Events are grouped into sessions: one task, across several apps. A Slack thread, a pull request and an editor session can belong to the same piece of work, and ALO keeps the reasons it connected them.

**Local storage.** Events, sessions and memories live in a database on your device, with retention you control.

**Memory on top.** Replays, decisions, open loops and "where you left off" are computed from sessions on the device.

**AI is optional and late.** When you ask for an AI feature, ALO builds the smallest context that answers the question, from sessions rather than raw events, and shows you exactly what would leave the device. You can use a local model, your own provider key, ALO AI, or nothing.

## On your Mac

The Mac app is a small menu bar agent. It observes focus changes through system notifications rather than polling, stores history in a local database, and serves its interface only on `127.0.0.1`. It has no network listener beyond the loopback interface.

## Across devices

Devices hold their own keys. Sync is designed as encrypted, device-to-device transfer of signed event bundles, with append-only history per device. A relay may help devices find each other and forward ciphertext; it cannot read it. Each device rebuilds its own indexes locally.
