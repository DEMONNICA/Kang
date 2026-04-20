> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [7.0.0]
>
> - Major overhaul of `service.sh` with universal `run_cmd` helper, power optimizations, thermal throttling bypass, dynamic trim memory, game performance mode for all third-party apps, pinner repin, and light doze.
> - Updated `post-fs-data.sh` to include Dalvik VM backup and optimization, and SurfaceFlinger property tuning.
> - Updated `action.sh` with CPU-intensive process detection via `top`, replaced `echo 3 > drop_caches` with `sysctl`, added `tune2fs` journal optimization, and improved comments.
> - Improved `uninstall.sh` with full restore support for kernel backup, Dalvik VM backup, SurfaceFlinger properties cleanup, and game mode reset.
> - Cleaned up `root` and `shell` by removing duplicate optimizations now handled by `service.sh`.
> - Added kernel parameter backup in `root` before applying optimizations for safer uninstallation.
> - Added display, animation, performance, game, and multitasking optimization via `settings put` in `service.sh`.
> - Added dynamic peak refresh rate detection to automatically set the highest supported refresh rate.
> - Fixed hardcoded `KANG` reference in `customize.sh` to use `$ID` variable.
> - Improved `customize.sh` with detailed sub-comments and fixed banner duplicate check.
> - And optimization and misc fixes.
---

> [6.6.6]
>
> - License Changes.
> - Changed the structure of `README.md` for a better impression.
> - Updated `customize.sh and verify.sh` for better future performance.
> - Simplify the `post-fs-data.sh` script by combining loops and removing irrelevant performance configuration.
> - Some changes and optimizations in `service.sh` for easier handling in the future.
> - Changed the binary names `NR -> shell` and `R -> root` for easier understanding.
> - Optimized `uninstall.sh` for cleaner uninstallation.
> - Improvements and updates to `action.sh` to get even better results.
> - And optimization And misc fixes.
---

> [6.0.0]
> 
> - Changes and improvements to `customize.sh and action.sh` handling for Plugins stability.
> - Changes and updates to `uninstall.sh and verify.sh` for easier and more stable operation.
> - Changes and updates to `post-fs-data.sh and service.sh` for better handling.
> - Disables and resets Binder call statistics (inter-process communication).
> - Disables various types of display logging.
> - Clears and stops collecting process statistics.
> - Reduced memory used for kernel tracing for `R`.
> - Reduced unnecessary window manager logs, saving resources for `NR`.
> - Added `disable_error_reporting` to reduce errors in sending error data.
> - Improved `surfaceflinger` optimization for even better ui and game experience.
---

> [5.0.0]
> 
> - Changed the previous version method storage `DEMONIC-PRJKT/version` now `.method`.
> - Kang in the current version only supports `AXM` 1.4.0 + cannot be used on version 1.3.*.
> - Moved `suppress_panic & silence_kernel` into `R` for root users, previously in `post-fs-data.sh`.
> - Reduce logging overhead, increase privacy, save battery.
> - Delete usage history, increase privacy, clear cache stats.
> - Fixed pid values piling up in version.
> - Disable overhead testing for HWUI filter.
> - Disable HWUI profiling and Set the HWUI debug level to 0 (disabled).
> - Disable capture of SKP (Skia Picture) files.
> - Disable dirty regions visualization and Disable layer updates visualization.
> - Disable tracing GPU resources.
> - Disable atrace for Skia and Disable Skia tracing.
> - Disable Perfetto track events for Skia.
> - Reduce system overhead and Improve UI rendering performance.
> - Removed `Android` detection in description.
> - And many more optimizations for the latest version.
---

> [4.0.0]
>
> - Dynamic banner usage for root and non-root users.
> - All plugin code has been fully updated for compatibility with both rooted and non-rooted devices.  
> - Overall detection accuracy has been enhanced and is now more reliable than in previous versions.  
> - Various minor fixes and property updates have been implemented to improve performance.  
> - The KANG feature is now smarter in detecting whether a device is rooted (R) or non-rooted (NR).  
> - The SETUP binary file has been removed; its functionality is now integrated and automatically adapts based on the device's root status (R or NR).
> - Removed the `system.prop` file which is no longer used in this version.
> - Numerous additional improvements have been made to further enhance overall stability.
> - I deleted the previous changelog, to make it look cleaner.
---