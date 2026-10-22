# User guide

## What is recorded

Edit History listens to Unity's serialized property modification notifications in **Edit Mode**. It stores object identity, recorded object/component names, serialized property path, and before/after text values. New records include property type metadata.

Different objects and properties have separate records. Within an active Undo group, pending slider edits keep the first before value and latest after value. A new Undo group or about 0.3 seconds of inactivity completes pending edits. Pausing a drag can therefore produce several entries; grouping is not guaranteed to match one mouse gesture.

Capture depends on Unity reporting modifications. Custom Inspectors or scripts bypassing normal serialization/Undo can produce no record. Play Mode changes are not recorded. This is not a complete audit of every project operation.

## Search and scopes

Open **Tools > Edit History > Search History**. **Ctrl/Cmd+F** focuses search. Results use newest recording order first, with the newest match initially selected.

Search matches literal text, ignoring case, across recorded object names, component names, serialized paths, before/after text, and object IDs. Empty text shows all entries in the scope. Regex, fuzzy matching, date filters, and operators are not supported. Names reflect recording time; renaming an object does not rewrite older records. Records have no timestamps or author identity.

| Control | Behavior |
| --- | --- |
| **Selection only** | Selected GameObjects and their components, or selected components/assets. Children are excluded. Scope follows selection. |
| Component **View history** | Pins scope to that component, or corresponding components in a multi-object Inspector. Selection changes do not clear it. |
| **Show all history** | Clears the component pin; other filters still apply. |
| **Advanced filter > Exact property path** | Matches one case-sensitive serialized path, such as `m_LocalPosition.x` or `age`. |
| **Reset filters** | Clears text, selection, exact-path, and pinned-component filters together. |

Object identities keep similarly named objects separate. Selection can include assets for searching; restore currently requires a component. To find one field, combine selection scope and its exact path, copied from **Technical details**.

## Read a change

Rows identify the recorded object, component, field, and compact **Before**/**After** previews. Details show full values, **Current value** when readable, and **Select object in Unity**. The text fields allow copying values. An empty string differs from missing recorded text.

**Technical details** contains the serialized path, object ID, and recorded property type. The object's saved scene must be open for scene-object selection/restoration; the tool does not open scenes automatically. Wide windows show details beside results; narrow windows stack them.

## Restore a field

Select an entry, compare before/after/current values, and click **Restore this value** under the desired side. **Before** is the value before that edit; **After** is its recorded result. **Already current** means that side matches the current serialized value.

The tool validates object, path, type, and value before assigning the chosen property through Unity's serialized editing and Undo system. Prefab instance restoration creates an instance override; it does not apply that override to the prefab source. Undo reverses restoration and Redo reapplies it. Restoration creates a new recorded edit.

Only the selected property is directly assigned. Your component's `OnValidate`, custom editor, or other callbacks may respond by changing additional state. Inspect the result as you would after a normal Inspector edit.

Restore covers component Boolean, integer, float/double, string, and ordinary numeric enum fields, including serialized private fields. Transform support is limited to individual local position/scale axes. See [compatibility](Compatibility.md) for rejected cases.

Legacy entries may lack original type metadata. A visible note explains that restore uses the current type. Changed enum meanings and old component schemas cannot be reconstructed.

## History versus scene state

Component counts mean recorded edits, not unsaved scene changes. Undo/Redo refreshes current values but does not promise a separate record for every Undo/Redo action. Scene saves and history saves are separate operations.

History survives a normal restart when its JSON save succeeds. It is local to the project, and does not replace backups or version control. See [data and privacy](DataAndPrivacy.md) for backup/reset instructions.
