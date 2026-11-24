# Releasing

One project: `unitcorn`. Pushing a `v*` tag publishes it, and the `Release`
workflow is the only thing that uploads.

One-time setup, on pypi.org (needs the account owner):

1. A trusted publisher for `unitcorn`: owner `noblecloud`, repository
   `UnitCorn`, workflow `release.yml`, environment `pypi`.
2. A `pypi` environment in the repo's GitHub settings.

Both are in place: the `v0.9.1` run published 0.9.1 through them.

Then: bump the version in `pyproject.toml`, merge to `main`,
`git tag v0.9.2 && git push origin v0.9.2`. PyPI rejects a file that already
exists, so never re-push a tag for a version that has already gone out.

The GitHub repo is `noblecloud/UnitCorn`; the old `WeatherUnits` URL redirects,
and a remote that still uses it keeps working.

`WeatherUnits` is retired and will not be updated. Its PyPI project stays at
0.8.0 — no shim, no further uploads.
