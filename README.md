# renovate-custom-manager-range-strategy

Minimal reproduction for a Renovate discussion (link below once filed).

Since Renovate 43.208.2, a custom regex manager that extracts a bare NuGet version gets no
updates, with or without an explicit `rangeStrategy`. The built-in nuget manager still
updates the same package.

All three files pin Cake.Tool `6.2.0`. Newer releases `6.3.0` and `7.0.0` exist.

| File | Manager | `rangeStrategy` |
|---|---|---|
| `.config/dotnet-tools.json` | nuget (control) | nuget manager default (`bump`) |
| `default.txt` | custom.regex | not set |
| `bump.txt` | custom.regex | `bump`, via `packageRules` |

## Current behavior

- `.config/dotnet-tools.json` gets updates to `6.3.0` and `7.0.0`.
- `default.txt` and `bump.txt` get no updates. Debug logs show `currentValue` `6.2.0` but
  `currentVersion` `7.0.0`.

Renovate 43.207.4 updates all three files.

## Expected behavior

All three files get updates to `6.3.0` and `7.0.0`, as in 43.207.4.

## Link to the Renovate issue or Discussion

To be added.
