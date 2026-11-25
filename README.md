# plogons

A custom Dalamud plugin repository. Plugin source code and release ZIPs live in
their own repositories; this repository hosts the index and plugin icons.

## Add the repository

In the Dalamud plugin installer, open **Settings**, find **Custom Plugin
Repositories**, and add this URL:

```text
https://raw.githubusercontent.com/wexxlee/plogons/main/repo.json
```

Save and enable the repository. The index is currently empty, so no plugins
will appear until one is published.

## Publish a plugin

1. Build the plugin in its source repository and publish a GitHub Release with
   a downloadable ZIP asset. The ZIP must contain `<InternalName>.dll` and
   `<InternalName>.json` at its root, plus any required dependencies.
2. Add the plugin's icon under `icons/`, using a unique filename.
3. Add an object to the array in `repo.json`, using the plugin's actual
   manifest values. Use the current Dalamud API level targeted by the build.
   Point both download links at the release ZIP, not the source-code archive.
4. Commit the icon and updated index. For later releases, update the version,
   download URLs, and any changed metadata together.
5. Add the repository in Dalamud and verify the plugin installs and loads.

For example, replace **every** placeholder below, including the example API
level, before adding an entry to `repo.json`:

```json
{
  "Author": "Your name",
  "Name": "Example Plugin",
  "InternalName": "ExamplePlugin",
  "AssemblyVersion": "1.0.0.0",
  "DalamudApiLevel": 0,
  "ApplicableVersion": "any",
  "Punchline": "A short description.",
  "Description": "What the plugin does.",
  "RepoUrl": "https://github.com/wexxlee/example-plugin",
  "IconUrl": "https://raw.githubusercontent.com/wexxlee/plogons/main/icons/example-plugin.png",
  "DownloadLinkInstall": "https://github.com/wexxlee/example-plugin/releases/download/v1.0.0/example-plugin.zip",
  "DownloadLinkUpdate": "https://github.com/wexxlee/example-plugin/releases/download/v1.0.0/example-plugin.zip"
}
```

`InternalName`, `AssemblyVersion`, and `DalamudApiLevel` must match the
published plugin. Keep release URLs version-specific so the index version and
downloaded package stay in sync. The raw icon URL must point to a committed
asset on `main`. Testing releases require their own testing version, API level,
and download URL; omit those fields if you are not publishing one.

The index is maintained manually; publishing a release in a plugin's repository
does not update it automatically. GitHub's raw-content cache can delay the
visibility of changes.
