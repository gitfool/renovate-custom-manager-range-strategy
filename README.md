# renovate-custom-manager-range-strategy

Minimal reproduction for [renovatebot/renovate#48077](https://github.com/renovatebot/renovate/discussions/48077).

Since Renovate 43.208.2, a custom regex manager that extracts a bare NuGet version gets no
updates, with or without an explicit `rangeStrategy`. The built-in nuget manager still
updates the same bare version.

All four files pin Cake.Tool `6.2.0`. Newer releases `6.3.0` and `7.0.0` exist.

| File | Manager | Versioning | `rangeStrategy` |
|---|---|---|---|
| `control.csproj` | nuget | nuget | nuget manager default (`bump`) |
| `.config/dotnet-tools.json` | nuget | semver | not set |
| `default.txt` | custom.regex | nuget | not set |
| `bump.txt` | custom.regex | nuget | `bump`, via `packageRules` |

`control.csproj` is the control for a bare NuGet version. `.config/dotnet-tools.json` only
shows the package lookup works, because the nuget manager reads it with semver versioning.

## Current behavior

- `control.csproj` and `.config/dotnet-tools.json` get updates to `6.3.0` and `7.0.0`.
- `default.txt` and `bump.txt` get no updates. Debug logs show `currentValue` `6.2.0` but
  `currentVersion` `7.0.0`.

Renovate 43.207.4 updates all four files.

## Expected behavior

All four files get updates to `6.3.0` and `7.0.0`, as in 43.207.4.

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/48077
