# History data and privacy

## Stored data and location

The current recorder writes **`EditHistory.json` in the project root**, beside `Assets`, `Packages`, and `ProjectSettings`. Installing the tool under `Assets/EditHistory` does not change that location.

Entries contain object ID, recorded object/component names, field path, before/after text, and, for new entries, field type metadata. There are currently no timestamps or author/account IDs.

**History is readable plain text.** A serialized string can contain a URL, token, internal name, or other sensitive value. The current recorder has no exclusion list, recording toggle, or encryption. Avoid entering secrets in recorded fields. Do not publish the JSON or attach it to public support reports.

The older **`EditHistory.jason`** filename is read only when the current JSON does not exist. It is a legacy import path, not a second active output. Leaving it behind after resetting the JSON can bring back a legacy entry.

## Network behavior

The current tool code contains no networking, account login, telemetry, or cloud synchronization. This applies to Edit History itself, not Unity Editor, the Asset Store, your project, or other packages. Visiting docs, downloading updates, and filing GitHub reports are separate online actions.

Local storage can still be shared by backup services, shared drives, source control, or support uploads.

## Persistence limits

Pending edits normally flush after about 0.3 seconds of inactivity, before assembly reload, during Editor shutdown, or when opening component history. A crash can occur before these callbacks.

The recorder rewrites the entire JSON file. It has no atomic replacement, backup rotation, retention cap, recovery, or corrupt-file quarantine. A malformed file disables recording for that load. A save failure leaves a warning and may leave recent edits only in memory; another edit triggers a retry.

Use scene backups and version control independently. History cannot recreate deleted objects, components, scripts, or scenes.

## Exclude history from Git

Add these rules to the Unity project's root `.gitignore`:

```gitignore
/EditHistory.json
/EditHistory.jason
```

Ignoring files does not remove copies already committed or exposed in older commits. Review Git history separately before making a project public.

## Back up or reset

1. Close the Unity project. Moving/deleting files while the recorder runs can be undone by a later flush.
2. Copy `EditHistory.json` and, if present, `EditHistory.jason` to a private backup location outside the project.
3. To reset history, move **both** files out of the project root, keeping the backups.
4. Reopen Unity. Empty history is written after the next recorded edit.

To restore a backup, close the project first and put that project's backed-up JSON in its original location. Use a matching complete project/scene backup if identities changed. There is no history merge feature.

## Uninstall

Back up needed history, then remove the imported `Assets/EditHistory` folder and let Unity recompile. The development checkout instead keeps implementation in `Assets/Editor`; preserve unrelated Editor scripts.

Uninstalling does not remove project-root JSON. Close Unity and move/delete those files separately if you no longer want them.
