> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [3.0.0]
>
> - KANG `plugins` banner changes.
> - Added backup mechanism for all modified global, secure, and system settings using `Backup.txt`.
> - Added backup for all modified `device_config` values using `device_config_backup.txt`.
> - Added dynamic CPU core detection for `dalvik.vm.dex2oat-cpu-set` based on `/proc/cpuinfo`.
> - Added error suppression (`>/dev/null 2>&1`) to fstrim commands and (`2>/dev/null`) to all prop sets.
> - Added existence checks for partitions in `fstrim_auto` before trimming.
> - Added new secure settings: `show_rotation_suggestions 0`, `double_tap_to_wake 1`, `tap_to_wake 1`.
> - Added new system setting: `footer_text_show 1`.
> - Changed `kernel_cpu_thread_reader` value to `"1000000000"` (previously not set).
> - Integrated dropbox settings into `put_global` with backup support (previously separate loop).
> - Improved `disable_debug_trace` and `system_tuner` to backup values before changes.
> - Removed obsolete debug commands: `cmd migard`, `cmd simpleperf`, `cmd atrace`, `cmd perfetto`, `cmd stats clear-puller-cache`.
> - Removed direct `dumpsys activity settings` grep loop (integrated into `system_tuner` with backups).
> - Added new AxManager package `frb.axeron.manager` to whitelist.
> - Added detailed log output when skipping whitelisted apps/processes.
> - Added secondary kill phase using `killall` for processes that survive `am kill-all`.
> - Changed `am kill-all` message to "Stop all non-whitelist background app processes".
> - Changed Telegram redirect from `https://t.me/modulkuntul` to `https://t.me/Demoniica`.
> - Improved cleanup accuracy by targeting remaining processes after `am kill-all`.
> - Added robust AxManager package detection (supports both `com.frb.axmanager` and `frb.axeron.manager`).
> - Added automatic fallback loop for future AxManager package name changes.
> - Added mandatory Axeron version check (requires `13100` or higher).
> - Changed image filename from `Kang.jpg` → `assets/KANG.jpg` (uppercase + moved to assets folder).
> - Changed AxManager requirement check from optional to mandatory with immediate abort if not met.
> - Improved `post-fs-data.sh` with safer kernel panic suppression using existence checks before applying `sysctl`.
> - Improved kernel log silencing by verifying writability of each `/sys` and `/proc` path before writing.
> - Changed all direct writes to conditional writes (`if writable/exists → then write`).
> - Prevented potential errors or permission denied spam on devices missing certain kernel parameters.
> - Maintained identical functionality while significantly increasing compatibility and stability across various devices/kernels.
> - Added creation of `system.prop` file with extensive debug property optimizations (e.g., disabling various debug flags like `debug.*, etc.).
> - Removed background execution of `SETUP` binary using `nohup` or `setsid`, along with PID file creation.
> - Improved debug suppression by setting multiple properties to disable logging, tracing, and other debug features in `system.prop`.
> - Added `restore_settings` function to revert global/secure/system settings from `Backup.txt` backup.
> - Added `restore_device_config` function to revert all device_config changes from `device_config_backup.txt`.
> - Added dynamic `resetprop` detection in `reset_dalvik_props` (supports root, Axeron binary, or system command).
> - Added `fstrim_auto` function for automatic filesystem trim on partitions (system, vendor, data, etc.).
> - Added error suppression (`2>/dev/null`) to all prop resets for cleaner execution.
> - Added existence checks in `fstrim_auto` before trimming partitions.
> - Changed main uninstall sequence to include restores, prop resets, and fstrim before file removal.
> - Removed `reset_debug_trace` function and its device_config/settings/stats resets.
> - Removed `reset_system_tuner` function and its activity_manager/runtime_native_boot resets and procstats clear.
> - Improved overall uninstall to fully restore device state including settings, configs, and filesystem maintenance.
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