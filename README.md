# Scanners for possible use of iOS required reason API

## Binary-based scanner (More complete)

This scanner looks for symbols in the binaries in given folder using `nm`.

It will find the `.app`, `.framework` and `.a` binaries.
Keep in mind that the symbols found in the app (`.app`) will be duplicated from the ones found in the static libraries `.a` since they are statically linked.

Usage:
`sh required_reason_api_binary_scanner.sh <Derived data directory>`

Example output:

```
sh required_reason_api_scanner_binary.sh \
~/Library/Developer/Xcode/DerivedData/DemoSymbols-aymfeypsyhqwfuaieijkrqdeohcd/Build/Products/Debug-iphonesimulator

> Analyzing binaries: ./DemoSymbols.app/DemoSymbols
> ---
> Used symbols in binary ./DemoSymbols.app/DemoSymbols: activeInputModes, fgetattrlist, fstat, fstatat, fstatfs, fstatvfs, getattrlist, getattrlistat, getattrlistbulk, lstat, mach_absolute_time, NSFileCreationDate, NSFileModificationDate, NSFileSystemFreeSize, NSFileSystemSize, NSURLContentModificationDateKey, NSURLCreationDateKey, NSURLVolumeAvailableCapacityForImportantUsageKey, NSURLVolumeAvailableCapacityForOpportunisticUsageKey, NSURLVolumeAvailableCapacityKey, NSURLVolumeTotalCapacityKey, NSUserDefaults, stat, statfs, statvfs, systemUptime
```

## Text-based scanner

The scan is very rudimentary and based on comparing strings, but should be very helpful for a first analysis.

Usage:

`sh required_reason_api_text_scanner.sh {directory_name}`

Example Output:

```
Found potentially required reason API usage 'UserDefaults' in './ViewController.swift'
Line numbers: 28
```

## Example project

In the directory `DemoSymbols` you will find a project that uses all the code that Apple asks for a required reason. It is used to test these scanners.

## Related docs to read

- https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_use_of_required_reason_api
- https://jochen-holzer.medium.com/embrace-the-evolution-preparing-your-ios-app-for-the-required-reason-api-38f2d12bbce5
- https://mastodon.social/@chockenberry/112095424613859371
