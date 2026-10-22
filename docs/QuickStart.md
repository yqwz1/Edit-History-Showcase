# Quick start

Use a copy of a project for your first trial. The current pre-release targets Unity **6000.3.9f1** in Edit Mode. [Check compatibility](Compatibility.md) before using another version.

## 1. Install

For an authorized pre-release `.unitypackage`, choose **Assets > Import Package > Custom Package**, select the package, and import its `Assets/EditHistory` folder. Wait for compilation to finish and resolve any Console compilation errors.

When released on the Unity Asset Store, import the product through **Window > Package Manager > My Assets** using the Unity account that acquired it. The public documentation repository does not include an installer or implementation.

No scene component, account registration, API key, render-pipeline change, or project settings change is needed. Recording starts automatically after Unity loads the scripts. It captures future edits; it cannot reconstruct changes made before installation.

When testing in the development project, the implementation is already in `Assets/Editor`. Do not import a second copy.

## 2. Record a first change

1. Open or create a scene and **save it before editing**, so scene objects have persistent identities.
2. Create an empty GameObject named `History Trial`.
3. In its Transform, change **Position X** from `0` to `3`. Commit the field by pressing Enter or leaving it.
4. Wait briefly. Pending edits complete after about **0.3 seconds of inactivity**; opening component history also flushes pending edits.
5. Open **Tools > Edit History > Search History** and search for `History Trial`.

Expected: an entry for `History Trial`, `Transform`, and its X position field, with **Before** `0` and **After** `3`. Unity may also report other axes; select the X entry.

## 3. Restore one value

1. Select the X position entry and compare **Before**, **After**, and **Current value**.
2. Under **Before**, click **Restore this value**. Position X should return to `0`.
3. Use Unity's **Edit > Undo**, then **Edit > Redo**, to reverse and reapply that restoration.

A matching value reads **Already current**. Restoration creates another history entry. Save the scene to persist the resulting scene change.

## 4. Open component history

The current pre-release adds an **Edit History** row below a component's Inspector header. **View history** pins the window to that component. Its context menu also includes **View Edit History**.

Use **Show all history** to leave the pinned scope, or **Reset filters** to clear all filters. The pre-release row depends on version-sensitive Unity internals; if unavailable, use the context menu or Tools menu. See [compatibility](Compatibility.md).

## 5. Protect recorded data

History is readable `EditHistory.json` beside your project's `Assets` folder. It can contain field values and object names. Do not publish it or attach it to a public issue. The current recorder has no retention cap or crash-safe replacement; read [data and privacy](DataAndPrivacy.md) before extended use.

Continue with the [user guide](UserGuide.md), or use [troubleshooting](Troubleshooting.md) for empty results and disabled restore buttons.
