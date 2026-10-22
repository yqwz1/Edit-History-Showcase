# Screenshot provenance

Captured on 22 October 2026 from the actual Edit History tool running in **Unity 6000.3.9f1 on Windows**.

The temporary demo project uses unchanged copies of the development tool's Editor scripts and stylesheet. Its `Player Tuning` component contains demonstration fields, and the recorder captures actual serialized edits before the screenshots are taken. The demonstration component and scene are not part of this public repository or the paid tool implementation.

- `history-overview.png`: recorded changes, component scope, and before/after/current comparison.
- `component-history.png`: the current pre-release's component entry point in the Unity Inspector.
- `restore-value.png`: current value after restoring a recorded value through the tool.

Images are direct window captures, cropped to the relevant tool or Inspector area. No interface is recreated or generated, and no displayed field values or controls are painted into an image. The restore screenshot follows an actual click of the tool's restore button: Move Speed changes from 7.25 to 4.5, and a new history entry records it. The current pre-release's Inspector integration is version-sensitive; see [compatibility](../docs/Compatibility.md).
