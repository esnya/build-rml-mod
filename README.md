# Build RML Mod

This GitHub Action builds a mod for ResoniteModLoader. It performs:

- Sets up the build environment.
  - MSBuild
  - SteamCMD
  - Resonite App
  - ResoniteModLoader
- Caches the build environment.
- Builds the mod.

## License

This project/action is licensed under the [MIT License](./LICENSE).



## Inputs

| **Input**       | **Description**                                                                 | **Default**                                                | **Required** |
|-----------------|---------------------------------------------------------------------------------|------------------------------------------------------------|--------------|
| `project`       | Path to the project directory.                                                  | `${{ github.workspace }}`                                  |              |
| `configuration` | Build configuration.                                                            | `Release`                                                  |              |
| `target-dir`    | Output directory for the build.                                                 | `${{ github.workspace }}/bin/${{ inputs.configuration }}`  |              |
| `steam-login`   | Login credentials for SteamCMD in the format `<username> <password>`.           |                                                            | Required     |
| `app-id`        | Steam App ID.                                                                   |                                                            |              |
| `cache-key`     | Cache key for the app.                                                          | `rml-mod-${{ inputs.app-id }}-${{ inputs.configuration }}` |              |

## Example Usage

```yaml
name: Build Mod

on:
  push:
    branches:
      - master

jobs:
  build:
    runs-on: windows-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Build Mod
        uses: esnya/build-rml-mod@v1
        with:
          project: ${{ github.workspace }}/YourProjectName
          steam-login: ${{ secrets.STEAMLOGIN }}
```
