# publish-script

## Usage

`pubnpm` and `pubbower` scripts are intended to be executed in the repository
folder immediately after `CHANGELOG.md` has been modified in preparation for the
release.

`pubnpm` is intended for repositories that are have only a `package.json` file
or both a `package.json` file and a `bower.json` file. If a `build` script
exists in `package.json` then `npm install` will be run before publishing.

`pubbower` is intended for repositories that have only a `bower.json` file.

Both scripts require a single argument, the release type, which is one of the
following: [patch | minor | major]

```shell
# a npm patch release
$ pubnpm patch

# a bower minor release
$ pubbower minor
```
`pubnpm` options:

* `-h` or `--help`: show help
* `-v` or `--verbose`: be verbose running commands
* `-n` or `--dry-run`: show commands that will be run without executing them
* `-t TAG` or `--tag TAG`: use the [npm publish](https://docs.npmjs.com/cli/publish) tag feature

The tag feature is useful if releasing to a "dev" branch vs the "latest":

```shell
$ pubnpm -v -t dev patch
```
