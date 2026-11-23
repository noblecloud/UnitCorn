# Releasing

Release order matters: `unitcorn` first, then the `WeatherUnits` shim, which depends on it.
The `Release` workflow does both in that order when a `v*` tag is pushed.

One-time setup, on pypi.org (needs the account owner):

1. Add a pending trusted publisher for `unitcorn` and another for `WeatherUnits`:
   owner `noblecloud`, repository `UnitCorn`,
   workflow `release.yml`, environment `pypi`.
2. Create a `pypi` environment in the repo's GitHub settings.

The `unitcorn` publisher is in place: the `v0.9.1` run published 0.9.1 through it.
The `WeatherUnits` publisher is not yet: that run's shim job failed with
`403 Invalid API Token: OIDC scoped token is not valid for project 'WeatherUnits'`.
Add the publisher, then re-run only the failed job — re-running the whole
workflow would try to upload 0.9.1 to `unitcorn` again, and PyPI rejects a file
that already exists.

Then: bump the version in `pyproject.toml` and `compat/WeatherUnits/pyproject.toml`,
merge to `main`, `git tag v0.9.1 && git push origin v0.9.1`.

The GitHub repo is `noblecloud/UnitCorn`; the old `WeatherUnits` URL redirects,
and a remote that still uses it keeps working.
