# publish-script

## Usage

The `pubnpm` script is intended to be executed in the repository folder
immediately after `CHANGELOG.md` has been modified in preparation for the
release.

`pubnpm` is intended for repositories that have a `package.json` file. If a
`build` script exists in `package.json` then `npm install` will be run before
publishing.

Both scripts require a single argument, the release type, which is one of the
following: [patch | minor | major]

```shell
# a npm patch release
$ pubnpm patch
```

`pubnpm` options:

* `-h` or `--help`: Show help.
* `-v` or `--verbose`: Be verbose running commands.
* `-C` or `--color=WHEN`:  Color mode: always, auto, never (default: `PUBNPM_COLOR` env var or `auto`).
* `-n` or `--dry-run`: Show commands that will be run without executing them.
* `-t TAG` or `--tag=TAG`: Use the [npm publish](https://docs.npmjs.com/cli/publish) tag feature
* `-b BRANCH` or `--branch=BRANCH`: Ensure running on a git branch (default: master, empty string to skip).
* `-N` or `--new`: Skip owner check for a new package.
* `-P` or `--public`: Used with `new` to specify that a scoped package is public.
* `-R` or `--restricted`: Used with `new` to specify that a scoped package is private/restricted.

**NOTE**: MacOS only supports short options.

The tag feature is useful if releasing to a "dev" branch vs the "latest":

```sh
pubnpm -v -t dev patch
```

### Release a new public scoped package from the main branch
```sh
pubnpm -N -P -b main major
```
