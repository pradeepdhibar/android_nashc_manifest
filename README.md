# LineageOS 23.2 for Realme 8 (nashc)

Device: Realme 8 4G  
Codename: nashc  
SoC: MediaTek MT6785  
Android: 16  
LineageOS: 23.2

## Source sync

Initialize LineageOS:

```bash
mkdir -p ~/android/lineage
cd ~/android/lineage

repo init \
  -u https://github.com/LineageOS/android.git \
  -b lineage-23.2 \
  --git-lfs
```

Add nashc local manifest:

```bash
mkdir -p .repo/local_manifests

curl -L \
  https://raw.githubusercontent.com/pradeepdhibar/android_nashc_manifest/lineage-23.2/default.xml \
  -o .repo/local_manifests/nashc.xml
```

Sync sources:

```bash
repo sync -c -j$(nproc) \
  --force-sync \
  --no-clone-bundle \
  --no-tags
```

## Build

```bash
cd ~/android/lineage
source build/envsetup.sh

lunch lineage_nashc-bp4a-userdebug

mka bacon -j6
```

ROM output:

```text
out/target/product/nashc/lineage-23.2-*-UNOFFICIAL-nashc.zip
```

## Notes

This source tree contains Android 16 compatibility changes for the legacy
MediaTek/Realme nashc platform.

The kernel contains additional BPF compatibility backports required for
Android 16 userspace.

This is an unofficial development build.
