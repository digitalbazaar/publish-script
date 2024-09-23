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
* `-b BRANCH` or `--branch=BRANCH`: Ensure running on a git branch (default: main, empty string to skip).
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
pubnpm -N -P major
```

### Release a new public scoped package from the master branch
```sh
pubnpm -N -P -b master major
```

# Releases at Digital Bazaar

Most / many repos here at DB are released via a in-house release process.

You can clone this repo somewhere and symlink the two pub* executables into ~/bin (or some custom location in your PATH).

You can tell if this tool is used by the presence of a DB styled changelog.md file in the root of a given repo.

## Cutting a deployment (via `pubtag`)

Running `pubtag` will result in an updated CHANGELOG.md and TWO new commits, which are automatically pushed back to main.
Note that this will require admin access on the repo to bypass main push protection.

If you are not an admin, you cannot push a release.

The process:

- Update CHANGELOG.md by replacing the date placeholders with the current date
  - NOTE: DO NOT create a manual commit
- Note the semver; note if this is a patch, minor or major update
- Run pubtag based on the type of update:
  - E.g., for a minor release, `pubtag minor`

Then, if successful you will observe new commits pushed to main and a packaging github action running against main.

Once completed, take the image artifact tag and revise the associated terraform repo to deploy.

### Failures

If there's a failure (e.g., insufficient permissions), you will need to reset some git history.
Check the latest commit on main before you ran the script.

Then do a hard reset:

```sh
git reset --hard COMMIT
```

Then, delete the tag:

```sh
git tag -d TAG
```

Where `tag` has the format `vMAJOR.MINOR.PATCH`.

You should be back to a clean state with local history matching the published repo.
