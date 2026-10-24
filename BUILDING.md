# Building Project World Music

Project World Music is a [GridlessSekai6](https://github.com/UnknownSekai/GridlessSekai6) custom project. This
page is for whoever builds the releases; players only need [INSTALL.md](INSTALL.md).

**Never publish game files**: not the game's APK, its asset zip, the Songs pack's contents or anything
extracted from them.

## What the build is made of

| Part | What it does |
|------|--------------|
| `scripts/build_all.sh` | the whole APK build, step by step |
| `scripts/build_master.py` | the game's master data: songs, cards, English names, no gacha/shop |
| `scripts/build_songs.py` | the Songs pack (every official song + its master data) |
| `scripts/build_extra_songs.py` | songs the game version lacks, from sonolus.sekai.best, Sbuga or sekai.best's asset mirror |
| `scripts/build_custom_vocals.py` | extra cover vocals (`data/custom_vocals.json`) |
| `scripts/fix_til.py` | adds the dummy speed entry the game needs to already-built charts |
| `scripts/build_title.py`, `make_title_image.py` | title screen (Retro background, Live2D, logo + version) |
| `scripts/build_attention.py` | the third boot screen (notice in EN/JA/KO) |
| `scripts/build_icons.py`, `make_icon.py` | the switchable app icons and shortcut icons |
| `scripts/make_manifest.py` | launcher activities, permissions, no Google Play Games |
| `java/pw/` | launcher, Chart Import, Card Maker, Co-op, App icon, debug panel |
| `native/pwnative.c` | native helper loaded into the running game (co-op start, results, Solo Live fix) |
| `converter/` | Sonolus level → custom chart converter (Chart Import and extra songs) |
| `data/` | English titles, artist/singer names, cover vocals list |

## Requirements

The build was made to run on the phone itself (Ubuntu under Termux/proot), but any Linux works. Paths in
`scripts/build_all.sh` assume the project is at `/root/gs6work` and the inputs in `/sdcard/Download`.

- Python 3 with `UnityPy`, `Pillow`, `cricodecs`, `rg-converters`, `astc-encoder-py`, `texture2ddecoder`
- Java 21 (`javac`), `tools/sdk/android.jar`, `tools/sdk/r8.jar`, `tools/uber-apk-signer.jar`
- `clang` + `lld` (the native helper), `ffmpeg`
- Your own copies of the game APK (`GS6.apk`) and its asset zip (`base_android.zip`)

## Commands

```
KEEP_ZIP=1 sh scripts/build_all.sh    # the APK, reusing the last asset zip (fast path)
sh scripts/build_all.sh               # also rebuilds the asset zip from base_android.zip
SONGS=1 sh scripts/build_all.sh       # also rebuilds the Songs pack
```

Extra songs and cover vocals are built separately, then picked up by the next build:

```
python3 scripts/build_extra_songs.py orig/assets/gridlesssekai6/masterdata_jp.json out/extra_songs [music id ...]
python3 scripts/build_custom_vocals.py out/masterdata_jp_songs.json out/custom_vocals
python3 scripts/update_songs_pack.py <old pack> out/masterdata_jp_songs.json <new pack> out/extra_songs/bundles out/custom_vocals/bundles
```

## Releasing

1. Set the version: `VERSION` in `scripts/make_title_image.py` (shown under the logo) and `DEST` in
   `scripts/build_all.sh` (the APK's file name).
2. Build, install, test.
3. Update [CHECKSUMS.md](CHECKSUMS.md) (`sha256sum` of the APK and the Songs pack) and upload both to the release.

## Notes

- Each script starts with a docstring saying what it does and how to run it.
- The app is marked debuggable, for testing on the phone.
- On Termux, the build runs on Termux's own Python: scripts stand in for UnityPy's audio helper
  (`fmod_toolkit`), which doesn't load on Android.
