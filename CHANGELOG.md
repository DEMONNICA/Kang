> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [8.5.0]
>
> - Added `device_config put` for `interaction_jank_monitor` and `latency_tracker` in `service.sh` to reduce background sampling overhead.
> - Added 13 missing global settings keys to the `settings delete` list in `uninstall.sh` (`sf_touch_timer_milliseconds`, `animator_duration_scale`, `force_hw_ui`, `fancy_ime_animations`, `tether_offload_disabled`, `enable_freeform_support`, `enable_non_resizable_multi_window`, `force_resizable_activities`, `development_enable_freeform_windows_support`, `background_activity_starts_enabled`, `hidden_api_policy`, `hidden_api_policy_pre_p_apps`, `hidden_api_policy_p_apps`) that were set by `service.sh` but never cleaned up on uninstall.
> - Added `min_refresh_rate`, `peak_refresh_rate`, `show_touches`, and `pointer_location` to the `settings delete system` list in `uninstall.sh` that were set by `service.sh` but never cleaned up on uninstall.
> - Added `settings delete global display_refresh_rate_in_zone` to `uninstall.sh` that was set by `service.sh` but never cleaned up on uninstall.
> - Added 10 missing `device_config` keys to the delete list in `uninstall.sh` (`runtime_native_boot disable_lock_profiling`, `runtime_native_boot iorap_readahead_enable`, `activity_manager data_sync_fgs_timeout_duration`, `activity_manager fgs_start_allowed_log_sample_rate`, `activity_manager fgs_start_denied_log_sample_rate`, `activity_manager max_cached_processes`, `activity_manager max_empty_time_millis`, `activity_manager max_phantom_processes`, `activity_manager media_processing_fgs_timeout_duration`, `activity_manager_native_boot use_freezer`) that were set by `root` but never cleaned up on uninstall.
> - Added `device_config delete` for `interaction_jank_monitor` and `latency_tracker` in `uninstall.sh` to clean up overrides on uninstall.
> - Added dynamic heap sizing in `post-fs-data.sh` based on device RAM from `/proc/meminfo` across four tiers.
> - Added dynamic `dex2oat-threads` in `post-fs-data.sh` based on actual CPU core count, capped at 6.
> - Added `SELF_PID` filter to top CPU deprioritization loop in `action.sh` to prevent the script from killing itself.
> - Added `dev.axora.manager` to root manager detection in `customize.sh`.
> - Added `$AXERON != "true"` guard at the top of `customize.sh` to abort installation if not run through Axeron/AxManager, before `ID` is even defined.
> - Added `tr -d '\r'` to module ID and name extraction in `verify.sh` to strip CRLF line endings.
> - Added `sha512`, `sha384`, `sha256`, and `sha224` to the hash algorithm fallback list in `verify.sh`; previously only `md5` and `sha1` were supported.
> - Changed `banner=` in `module.prop` from local asset path to remote GitHub URL.
> - Changed `strings` grep pattern in `customize.sh` from `manager|pure` to `axora|pure|manager`.
> - Changed `customize.sh` to merge `get_app_label()` into `check_axeron_requirement()` using a `for entry in "pkg:label"` loop; `aapt` is no longer used for root manager label detection.
> - Changed `customize.sh` to remove `AXMPATH` and `AXMPROP` variables in favor of the literal `$AXERONDIR/plugins/$ID` path.
> - Changed `customize.sh` to remove `IS_ROOTED` and `CURRENT_USER` variables in favor of direct `$USER = "root"` checks.
> - Changed `customize.sh` to always re-detect the root manager and overwrite `.method` instead of reading a cached value.
> - Changed `.method` line 3 in `customize.sh` to store `$AXERONVER` instead of the root manager app's versionCode.
> - Changed `set_permissions()` in `customize.sh` to use `find -print0 | while read -d ''` instead of `for path in $(find ...)` for safer handling of filenames with spaces.
> - Changed `top` output in `action.sh` to store in variable first with fallback to `top -n 1` for devices that do not support `-b` flag.
> - Changed `post-fs-data.sh` to always set atrace and Skia tracing properties regardless of whether they existed before.
> - Changed `heaptargetutilization` in `post-fs-data.sh` from `0.5` to `0.75` to avoid excessive GC.
> - Changed `grep -oP` in `service.sh` to `awk` for process name parsing; `-P` flag is not supported by toybox grep.
> - Changed `[ -n "$BIN_FILE" ]` to `[ -x "$BIN_FILE" ]` in `service.sh` to also verify the binary is executable before running.
> - Changed Dalvik VM backup in `post-fs-data.sh` to only save properties that have a value; properties absent before installation are deleted on uninstall without a sentinel.
> - Changed `uninstall.sh` Dalvik restore to delete properties not found in backup instead of reading a sentinel value.
> - Changed `root` sub-comments from `#0–#12` to `#1–#15` with more descriptive labels; split former `#8` into three separate numbered sections.
> - Fixed `printk` backup in `root` separated from kernel param loop; value normalized from tab-separated to space-separated for consistency with restore.
> - Fixed kernel parameter backup in `root` to skip entries with empty values, preventing blank lines in the backup file.
> - Fixed PID validation in `uninstall.sh` to prevent `kill -9` from running without arguments if PID file is empty.
> - Fixed `nohup am start` placed inside `while` loop in `customize.sh`; moved outside so Telegram is opened only once.
> - Fixed device name substitution in `customize.sh` to skip `name=` update if `$DEVICE_NAME` is empty, preventing `name=Kang for` with trailing space.
> - Fixed `check_axeron_requirement()` in `customize.sh` to `return 1` and abort installation if neither `AxManager` nor `Axora` is detected, instead of silently continuing with an empty `.method` file.
> - Fixed vmstat variables in `action.sh` — `cache`, `so`, and `free` now default to `0` if vmstat output is empty or unavailable.
> - Fixed `sleep 1` added after `am force-stop` in `action.sh` to allow processes to fully terminate before `pidof`.
> - Fixed division by zero in `service.sh` when `/proc/meminfo` is unavailable; `MEM_TOTAL` and `MEM_AVAIL` now default to safe values.
> - Fixed stale runtime `description=` text in `service.sh` that overwrote `module.prop` on every boot with outdated wording; now matches the current description and uses `|` instead of `•` as separator.
> - Removed `.method` file deletion from `uninstall.sh`; only the plugin directory is removed on uninstall.
> - Removed `$LOGNAME` check in `service.sh` user detection; `$USER` alone is now used.
> - Removed duplicate SurfaceFlinger property deletion block in `uninstall.sh`; already covered by the debug property reset loop.
> - Removed `assets/KANG01.jpg` and `assets/KANG02.jpg` from ZIP extraction in `customize.sh`.
> - Removed `get_app_label()` function from `customize.sh`; `aapt` is no longer used.
> - Removed minimum `$AXERONVER` (14000) version requirement check from `customize.sh`.
> - Removed `.sha`/`.md5` hash file cleanup step from `customize.sh`.
> - Removed `zip=$(clean_path "$zip")` sanitization in `extract()` in `verify.sh`; zip path is no longer cleaned before use.
> - Removed `tune2fs` journal optimization from `action.sh`.
> - Removed CPU core count cap of 8 in `post-fs-data.sh` to support devices with more than 8 cores.
---

> [7.0.0]
>
> - Added kernel parameter backup in `root` before applying optimizations for safer uninstallation.
> - Added display, animation, performance, game, and multitasking optimization via `settings put` in `service.sh`.
> - Added dynamic peak refresh rate detection to automatically set the highest supported refresh rate.
> - Changed `service.sh` with universal `run_cmd` helper, power optimizations, thermal throttling bypass, dynamic trim memory, game performance mode for all third-party apps, pinner repin, and light doze.
> - Changed `post-fs-data.sh` to include Dalvik VM backup and optimization, and SurfaceFlinger property tuning.
> - Changed `action.sh` with CPU-intensive process detection via `top`, replaced `echo 3 > drop_caches` with `sysctl`, added `tune2fs` journal optimization, and improved comments.
> - Changed `uninstall.sh` with full restore support for kernel backup, Dalvik VM backup, SurfaceFlinger properties cleanup, and game mode reset.
> - Changed `customize.sh` with detailed sub-comments and fixed banner duplicate check.
> - Changed `root` and `shell` by removing duplicate optimizations now handled by `service.sh`.
> - Fixed hardcoded `KANG` reference in `customize.sh` to use `$ID` variable.
---

> [6.6.6]
>
> - Changed the structure of `README.md` for a better impression.
> - Changed the binary names `NR -> shell` and `R -> root` for easier understanding.
> - Changed `customize.sh` and `verify.sh` for better future performance.
> - Changed `post-fs-data.sh` by combining loops and removing irrelevant performance configuration.
> - Changed `uninstall.sh` for cleaner uninstallation.
> - Changed `action.sh` for better results.
> - Changed license from GNU General Public License to Apache License 2.0.
---

> [6.0.0]
>
> - Added `disable_error_reporting` to reduce errors in sending error data.
> - Changed `customize.sh` and `action.sh` handling for Plugins stability.
> - Changed `uninstall.sh` and `verify.sh` for easier and more stable operation.
> - Changed `post-fs-data.sh` and `service.sh` for better handling.
> - Changed Binder call statistics to disabled and reset (inter-process communication).
> - Changed display logging to disabled.
> - Changed process statistics collection to cleared and stopped.
> - Changed kernel tracing memory limit for `R`.
> - Changed window manager log verbosity for `NR`.
> - Changed `surfaceflinger` optimization for better UI and game experience.
---

> [5.0.0]
>
> - Changed version method storage from `DEMONIC-PRJKT/version` to `.method`.
> - Changed minimum supported `AXM` version to 1.4.0+; version 1.3.* is no longer supported.
> - Changed `suppress_panic` and `silence_kernel` to run in `R` only, previously in `post-fs-data.sh`.
> - Changed logging overhead to reduced for lower battery usage and increased privacy.
> - Changed usage history to cleared on boot for increased privacy and clean cache stats.
> - Changed HWUI overhead testing, profiling, and debug level to disabled.
> - Changed SKP (Skia Picture) file capture to disabled.
> - Changed dirty regions and layer updates visualization to disabled.
> - Changed GPU resource tracing to disabled.
> - Changed atrace, Skia tracing, and Perfetto track events for Skia to disabled.
> - Fixed pid values piling up in version.
> - Removed `Android` detection in description.
---

> [4.0.0]
>
> - Added dynamic banner usage for root and non-root users.
> - Changed all plugin code for compatibility with both rooted and non-rooted devices.
> - Changed root/non-root detection accuracy for more reliable results.
> - Changed KANG root detection logic for smarter `R` and `NR` identification.
> - Removed SETUP binary; functionality now integrated and adapts automatically based on root status.
> - Removed `system.prop` file which is no longer used in this version.
---

> [3.0.0]
>
> - Added backup mechanism for all modified global, secure, and system settings using `Backup.txt`.
> - Added backup for all modified `device_config` values using `device_config_backup.txt`.
> - Added dynamic CPU core detection for `dalvik.vm.dex2oat-cpu-set` based on `/proc/cpuinfo`.
> - Added new secure settings: `show_rotation_suggestions 0`, `double_tap_to_wake 1`, `tap_to_wake 1`.
> - Added new system setting: `footer_text_show 1`.
> - Added new AxManager package `frb.axeron.manager` to whitelist.
> - Added detailed log output when skipping whitelisted apps and processes.
> - Added secondary kill phase using `killall` for processes that survive `am kill-all`.
> - Added robust AxManager package detection supporting both `com.frb.axmanager` and `frb.axeron.manager`.
> - Added automatic fallback loop for future AxManager package name changes.
> - Added mandatory Axeron version check requiring `13100` or higher.
> - Added `system.prop` file with extensive debug property optimizations.
> - Added `restore_settings` function to revert global, secure, and system settings from `Backup.txt`.
> - Added `restore_device_config` function to revert all `device_config` changes from `device_config_backup.txt`.
> - Added dynamic `resetprop` detection in `reset_dalvik_props` supporting root, Axeron binary, or system command.
> - Added `fstrim_auto` function for automatic filesystem trim on partitions.
> - Changed banner in `plugins`.
> - Changed `kernel_cpu_thread_reader` value to `1000000000`.
> - Changed dropbox settings into `put_global` with backup support.
> - Changed `disable_debug_trace` and `system_tuner` to backup values before changes.
> - Changed `am kill-all` message to "Stop all non-whitelist background app processes".
> - Changed Telegram redirect from `https://t.me/modulkuntul` to `https://t.me/Demoniica`.
> - Changed cleanup to target remaining processes after `am kill-all`.
> - Changed image filename from `Kang.jpg` to `assets/KANG.jpg`.
> - Changed AxManager requirement from optional to mandatory with immediate abort if not met.
> - Changed `post-fs-data.sh` with safer kernel panic suppression using existence checks before applying `sysctl`.
> - Changed kernel log silencing to verify writability of each `/sys` and `/proc` path before writing.
> - Changed all direct writes to conditional writes.
> - Changed main uninstall sequence to include restores, prop resets, and fstrim before file removal.
> - Removed obsolete debug commands: `cmd migard`, `cmd simpleperf`, `cmd atrace`, `cmd perfetto`, `cmd stats clear-puller-cache`.
> - Removed direct `dumpsys activity settings` grep loop; integrated into `system_tuner` with backups.
> - Removed background execution of `SETUP` binary using `nohup` or `setsid`, along with PID file creation.
> - Removed `reset_debug_trace` function and its `device_config`, settings, and stats resets.
> - Removed `reset_system_tuner` function and its `activity_manager`, `runtime_native_boot` resets, and procstats clear.
---

> [2.0.0]
>
> - Added `action.sh` to extracted file list with executable permission (`0755`).
> - Added cleanup of legacy files: auto-delete stray `SETUP` binaries and old `KANG` directories across `$AXERONDIR`.
> - Added silent background launch of Telegram channel via `nohup am start` after installation.
> - Added dynamic random emoji to author line in `module.prop`.
> - Added `action.sh` to force-stop all third-party apps while whitelisting `com.frb.axmanager` and `com.termux`, then run `am kill-all`.
> - Added loop to disable FGS sampling rates.
> - Added full Dropbox logging disable.
> - Changed all installation paths to `$AXERONDIR` from `/data/data/com.android.shell/AxManager`.
> - Changed `ZIPFILE` location to `/data/local/tmp/AxManager/zip/module.zip`.
> - Changed random devil message pool from 12 to 15 entries.
> - Changed `service.sh` to use `$AXERONDIR` paths and new version file location.
> - Changed `service.sh` PID handling to remove old PID sparkles before appending new one.
> - Changed `uninstall.sh` to use `$AXERONDIR` paths and remove leftover `DEMONIC-PRJKT` folder and stray `SETUP` in `$AXERONDIR/xbin`.
> - Changed `apply_dalvik_props()` with robust `resetprop` detection supporting root, `$AXERONBIN/resetprop`, and find-based fallback.
> - Fixed success notification quoting to prevent shell injection on module names containing spaces.
> - Removed redundant `.vunzip` extraction from verification flow.
> - Removed outdated settings from `put_system()`: `chip 1`, `font_scale 0.85`, `screen_off_animation 1`, `screen_off_timeout 60000`.
---

> [0.5.0]
>
> - Initial release.
---