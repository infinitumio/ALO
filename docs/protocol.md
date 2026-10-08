# ALO Protocol (`alo/1`)

> Status: draft. The format below is the one ALO's core is built around. Public SDKs are planned, and the local endpoint in current Mac builds accepts a smaller earlier format.

`alo/1` is a small event format for telling ALO that something happened. Applications emit events locally, to the ALO agent on the same machine. Events never go to the internet.

```json
{
  "protocol": "alo/1",
  "type": "task.completed",
  "source": "github",
  "project": "atlas",
  "entity": "PR #184",
  "ts": 1791346500,
  "duration": 0,
  "metadata": { "issue": "ATLAS-184" }
}
```

## Fields

| Field | Type | Notes |
| --- | --- | --- |
| `protocol` | `"alo/1"` | Required |
| `type` | string | Dotted verb, such as `commit.created`, `document.edited`, `task.completed` |
| `source` | string | The app or connector, such as `github`, `slack`, `figma` |
| `ts` | number | Epoch seconds |
| `project` | string? | The project this belongs to, if known |
| `entity` | string? | What it is about: a file name, issue or channel, never its contents |
| `duration` | number? | Seconds, up to one day |
| `metadata` | object? | Up to 16 flat keys of string, number or boolean |

## Philosophy

- **Small.** An event is a sentence, not a document.
- **Structured.** Dotted types and bounded fields make events comparable across apps.
- **Local.** Events go to the agent on the same device. Nothing is sent to ALO.
- **Privacy-aware.** Keys that look like content (`body`, `text`, `message`, `password`, `token`, `url`, `path` and similar) are refused, not stored.
- **Extensible.** New apps add new types without changing the format.

## Example

```ts
// Planned SDK. Talks to the ALO agent on this machine.
alo.event({
  type: "task.completed",
  project: "atlas",
  metadata: { issue: "ATLAS-184" },
})
```

The long-term goal is a common private activity layer between applications and personal AI. Ideas and integration requests are welcome in [Issues](https://github.com/infinitumio/ALO/issues/new/choose).
