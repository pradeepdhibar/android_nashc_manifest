# crDroid Android 16 for Realme 8 (nashc)

Device: Realme 8 4G  
Codename: `nashc`  
SoC: MediaTek MT6785  
Android: 16  
ROM: crDroid 12.x

This branch contains the local manifest used for the crDroid Android 16 nashc build tree.

## Manifest branch

Use:

```text
crdroid-16-nashc
```

The manifest keeps nashc-specific framework patches in dedicated crDroid branches while device-specific trees continue to use the `lineage-23.2-nashc` branches.

### crDroid-side patch branches

The following repositories track `crdroid-16-nashc`:

- `frameworks/base`
- `frameworks/native`
- `external/selinux`
- `system/netd`
- `system/vold`

These branches preserve the nashc Android 16 compatibility and device fixes on top of the crDroid source base.

### Device-specific branches

The following nashc/device repositories track `lineage-23.2-nashc`:

- `device/realme/nashc`
- `vendor/realme/nashc`
- `device/mediatek/sepolicy_vndr`
- `frameworks/opt/telephony`
- `hardware/lineage/interfaces`
- `hardware/mediatek`
- `hardware/oplus`

The kernel and legacy LiveDisplay dependency remain pinned to tested commits in `default.xml`.

## Add the local manifest

From an already initialized crDroid Android 16 source tree:

```bash
mkdir -p .repo/local_manifests

curl -L \
  https://raw.githubusercontent.com/pradeepdhibar/android_nashc_manifest/crdroid-16-nashc/default.xml \
  -o .repo/local_manifests/default.xml
```

## Sync

Normal sync:

```bash
repo sync -c \
  -j4 \
  --no-clone-bundle \
  --no-tags \
  --fail-fast
```

Do **not** use global `--force-sync` for routine updates. If repo reports a checkout/object-store migration conflict, inspect that project first and only use selective `--force-sync` after confirming the worktree is clean and its custom commits are safely pushed.

## Updating crDroid

For a new crDroid update:

1. Sync/update the upstream crDroid source.
2. Update the dedicated `crdroid-16-nashc` branches while preserving the nashc patches.
3. Keep device/vendor changes on their `lineage-23.2-nashc` branches.
4. Verify the resolved manifest and all custom heads before building.
5. Build and test before moving any intentionally pinned dependency.

## Important nashc fixes currently preserved

The custom branches include device-specific Android 16 compatibility work such as legacy-kernel framework compatibility, SELinux compatibility, tethering/netd fixes, and other nashc-specific framework changes.



## Notes

This is an unofficial development setup for Realme 8 4G (`nashc`). The manifest is intended to make crDroid updates reproducible while keeping device patches separated from upstream source history.
