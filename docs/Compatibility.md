# Compatibility and limitations

**Pre-release development target: Unity 6000.3.9f1.** The project and validation runner use that version. Other Unity releases, macOS, and Linux require separate checks before support is advertised. Current development uses Windows.

The implementation lives in an `Editor` folder. It is an Editor workflow tool, not runtime/gameplay recording. Its code does not reference URP, HDRP, Input System, or third-party libraries. Template packages from the development project are not dependencies of the staged tool.

## Capture and restore coverage

A searchable row does not imply safe restoration support.

| Field or edit | Current behavior |
| --- | --- |
| Component serialized Boolean, integer, float/double, string | Captures reported modifications; individual restore supported. |
| Serialized private component field | Supported when Unity exposes a supported serialized property. |
| Ordinary numeric enum | Numeric restore supported; old enum meanings are not reconstructed. |
| Transform local position/scale X/Y/Z | Individual axis restoration supported. |
| Transform rotation or other Transform paths | Restore rejected. |
| Prefab instance field | Supported restore creates an instance override. Complete Prefab Mode/source-asset coverage is not established. |
| Multiple selected components | Capture keeps targets separate; each restore applies to the selected entry. |
| Object references | No dedicated history representation; restore rejected. |
| Arrays/lists, elements, sizes | Restoration rejected even when text was recorded. |
| Vectors, colors, bounds, curves, quaternions, managed references | No general restore support. The explicit Transform axis exceptions above apply. |
| ScriptableObject/non-component asset | May be captured/searchable; restoration rejects non-components. |
| Script assignment (`m_Script`) | Restore rejected. |
| Added/removed components, deleted objects, hierarchy restructuring | No structural recovery. |
| Missing, read-only, renamed, or type-changed field | Restore rejected when validation detects the mismatch. |
| Unsaved scene identity | Restore rejected. Save the scene before recording an edit you need later. |
| Closed scene / deleted component | Cannot restore an unresolved target; opening its saved scene may resolve it. |
| Play Mode | Capture and restore disabled. |
| Custom Inspector bypassing serialization/Undo | Capture not guaranteed. |

## Inspector integration

The current component history row reflects Unity's internal `EditorElement` structure. When unavailable, it emits one warning; the Tools window and component context menu remain available.

This is an **Asset Store release blocker**: [Unity's submission guidelines, section 2.5.g](https://assetstore.unity.com/publishing/submission-guidelines) prohibit reflected internal Editor APIs. Replace that integration with supported APIs before submission. Its behavior here describes the pre-release, not a promise for the store version.

## Storage and scale

Current storage is project-root JSON with whole-file rewrites. There is no retention cap, exclusion list, pause control, atomic replacement, or corruption recovery. Malformed history stops recording for that load and displays an error. Failed saves can leave changes only in memory.

Search uses an in-memory index and virtualized list. No large-project benchmark, maximum record count, or crash-recovery guarantee is claimed. See [data and privacy](DataAndPrivacy.md).
