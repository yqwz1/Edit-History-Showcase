# Troubleshooting

Start in Edit Mode with the correct saved scene open. Read the Console and the history window's warning before changing files.

| Symptom | Check or action |
| --- | --- |
| No menu | Wait for compilation, fix project compilation errors, and keep exactly one copy in an `Editor` folder. |
| Duplicate type errors | An older/development copy may remain in `Assets/Editor`. Back up, then keep one implementation. |
| No edits | Make a new serialized Inspector edit in Edit Mode and commit it. Earlier edits cannot be reconstructed. Check storage errors and custom Inspector behavior. |
| No matching results | Use **Reset filters**. Text, path, selection, or pinned scopes may hide entries. Selection excludes children. |
| Selection changes but scope stays fixed | Component history is pinned. Use **Show all history** or **Reset filters**. |
| Exact filter matches nothing | Copy the case-sensitive serialized path from **Technical details**; a displayed label can differ. |
| No component history row | Use context menu **View Edit History** or the Tools menu. The pre-release row depends on Unity internals. |
| Restore disabled | Read the message/button tooltip. Type, path, object, scene identity, or recorded value may be unsupported. |
| **Already current** | That side already matches the field. Choose another value/entry. |
| Component unavailable | Open its saved scene. Deleted/recreated objects have different identities and are not recreated. |
| Unsaved scene identity | Save, then make a new edit. Saving cannot repair an older unsaved-scene record. |
| Type changed / missing field | Review script/schema changes. No automatic historical migration is provided. |
| Reference, array, rotation, or asset restore rejected | See the supported-type table in [compatibility](Compatibility.md). |
| Custom Inspector edits missing | Reproduce using a standard serialized field; the custom Inspector may bypass modification notifications. |
| **History could not be loaded** | Preserve the JSON. Close Unity, back up/move both history filenames, and reopen to start clean. No automatic repair exists. |
| Memory edits could not be saved | Check permissions, read-only flags, disk space, and Console exception. Correct the cause, then make an edit to retry. Restarting can lose memory-only entries. |
| Old entry returns after reset | The legacy filename may remain. Follow [two-file reset instructions](DataAndPrivacy.md). |
| Window layout is difficult to read | Widen it or scroll each panel. Keep `EditHistoryWindow.uss` beside `EditHistoryWindow.cs`. |

Follow [support](Support.md) for reproducible problems. Send sanitized steps/error text, not full history, paid source, or your entire project.
