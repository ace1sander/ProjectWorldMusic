# Installing Project World Music

You'll need an **arm64 Android** phone or tablet and about **6 GB** free.

| Download | Size | |
|----------|-----:|---|
| `Project World vX.YY.apk` | ~1.7 GB | the app |
| Songs pack (`.zip`) | ~2.4 GB | every song. Without it you only get one |

Get the Songs pack from a mirror: **[Pixeldrain](https://pixeldrain.com/u/xW5D8kJi)** (more mirrors will be added).

Checksums: [CHECKSUMS.md](CHECKSUMS.md)

---

## 1 · The app

Install the APK (let your browser or file manager install apps if Android asks). Updating? Install
over the old version; your progress stays.

## 2 · The songs

Put the Songs pack zip, **as it is, not unzipped**, in:

```
Download/ProjectWorld/Songs/
```

Create the folders if they're not there. Keep just **one** zip in that folder; any file name works.

## 3 · First start

Open Project World Music and allow **All files access** when it asks (that's how it reads your songs and
charts). The first start after installing or updating unpacks the game, with a progress bar, which takes a
minute or two. Then tap the title screen and play. 🎶

---

## 📥 Custom charts

**Have chart files?** Drop `.android.chart.gs6` files into `Download/ProjectWorld/Charts/` and restart.
They're in **Solo Live › Custom**. Delete a file to remove its chart.

**Want to import from Sonolus?**
1. Install [Termux](https://f-droid.org/en/packages/com.termux/) from F-Droid or GitHub (the Play Store
   version won't work).
2. Long-press the Project World Music icon → **Import Chart**.
3. First time only: **Copy setup command** → **Open Termux** → paste → Enter → **Allow**. It runs for
   10–20 minutes (about 2.5 GB) and finishes with `== Done`.
4. Paste a chart link, tap **Convert**, then **Done**, and open the game again.

Changed your mind? Import Chart → **Remove converter**.

## 👥 Co-op

Same Wi-Fi, same Songs pack, everyone on Project World Music. One player makes a room in **Live › Co-op**, the
others join.

## 🎨 App icon

Long-press the icon → **App icon**.

---

## Something wrong?

| What you see | Try this |
|--------------|----------|
| Only one song | Songs pack not in `Download/ProjectWorld/Songs/`, or All files access is off (Settings › Apps › Project World Music) |
| Stuck while unpacking | Free up some space and open the app again |
| "Termux didn't start the converter" | Open Termux once, then try again; on Xiaomi/HyperOS let Termux run in the background |
| It crashed | Open it again: it shows what went wrong. Then see [BUG_REPORTS.md](BUG_REPORTS.md) |
