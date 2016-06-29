# publish-script

## Usage

`pubnpm` and `pubbower` scripts are intended to be executed in the repository
folder immediately after `CHANGELOG.md` has been modified in preparation for the
release.

`pubnpm` is intended for repositories that are have only a `package.json` file
or a `package.json` file and a `bower.json` file.

`pubbower` is intended for repositories that have only a `bower.json` file.

Both scripts require a single argument, the release type, which is one of the
following: [patch | minor | major]

```
// a npm patch release
pubnpm patch

// a bower minor release
pubbower minor
```
