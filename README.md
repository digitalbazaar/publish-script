# publish-script

## Usage

`pubnpm` and `pubbower` scripts are intended to be executed in the repository
folder immediately after `CHANGELOG.md` has been modified in preparation for the
release.

Both scripts require a single argument, the release type, which is one of the
following: [patch | minor | major]

```
// a npm patch release
pubnpm patch

// a bower minor release
pubbower minor
```
