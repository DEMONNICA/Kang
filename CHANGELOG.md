> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [2.0.0]
>
> - Switched all installation paths to `$AXERONDIR` (from `/data/data/com.android.shell/AxManager`) for full compatibility with the latest AxManager non-root mode.  
> - Updated `ZIPFILE` location to `/data/local/tmp/AxManager/zip/module.zip` to match new temporary storage behavior.  
> - Added aggressive cleanup of legacy files: auto-delete stray `SETUP` binaries and old `KANG` directories across the entire `$AXERONDIR`.  
> - Expanded extracted file list: now includes `action.sh` as a required and executable component.  
> - Made `action.sh` executable (`0755`) alongside `SETUP` and `uninstall.sh` during permission phase.  
> - Increased random devil message pool from 12 to 15 entries (added Adramelech, Lucifugus, Lucius).  
> - Added silent background launch of Telegram channel (`https://t.me/modulkuntul`) via `nohup am start` after successful installation and after running `action.sh`.  
> - Refined success notification with proper quoting to prevent shell injection on module names containing spaces.  
> - Streamlined verification flow: removed redundant `.vunzip` extraction for `customize.sh` itself.  
> - Updated `service.sh` to use `$AXERONDIR` paths and new version file location.  
> - Improved `service.sh` PID handling: now removes old PID sparkles before appending new one (`sed -i -E 's/ \([0-9]+ ✨\)//g'`).  
> - Added dynamic random emoji to author line in `module.prop` (tasty_face, fox_face, bear_face, rabbit_face) via `get_random_emoji()`.  
> - Reworked `uninstall.sh`: now uses `$AXERONDIR` paths and removes leftover `DEMONIC-PRJKT` folder + stray `SETUP` in `$AXERONDIR/xbin`.  
> - Added new `action.sh`: force-stops all third-party apps (`pm list packages -3`) while whitelisting `com.frb.axmanager` and `com.termux`, then runs `am kill-all` and opens Telegram channel in background.  
> - Added loop to disable FGS sampling rates (`fgs_start_allowed_log_sample_rate`, `fgs_start_denied_log_sample_rate`, `fgs_atom_sample_rate`, `compact_statsd_sample_rate`, `freeze_statsd_sample_rate` → 0).  
> - Added full Dropbox logging disable (`dropbox_age_seconds`, `dropbox_max_files`, `dropbox_quota_kb`, `dropbox_quota_percent` → 0).  
> - Removed outdated settings from `put_system()`: `chip 1`, `font_scale 0.85`, `screen_off_animation 1`, `screen_off_timeout 60000`.  
> - Enhanced `apply_dalvik_props()` with robust `resetprop` detection: supports root, `$AXERONBIN/resetprop`, and `find`-based fallback with proper error handling and return codes.  
> - Minor cleanup: consistent variable naming, safer path handling, better indentation across all scripts.
---

> [1.5.0]
>
> - A major total change across the board.
---

> [0.5.0] `BETA`
>
> - Initial release.
---