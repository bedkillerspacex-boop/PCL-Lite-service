# PCL Lite Plugin Marketplace

The launcher reads [`index.json`](index.json) from this repository's `main` branch.
The index is intentionally static: plugin packages are hosted as assets on each plugin's GitHub Release.

## Add a plugin

1. Publish a `.pclplugin` package as an asset on a public GitHub Release.
2. Compute the SHA-256 digest of the exact downloaded package file.
3. Add an entry to `index.json` and submit it in a pull request.

Example:

```json
{
  "schemaVersion": 1,
  "plugins": [
    {
      "id": "example.hello",
      "name": "Hello Plugin",
      "version": "1.0.0",
      "author": "Plugin author",
      "description": "A short description shown in the launcher.",
      "packageUrl": "https://github.com/example/hello-plugin/releases/download/v1.0.0/hello.pclplugin",
      "website": "https://github.com/example/hello-plugin",
      "sha256": "REPLACE_WITH_64_HEXADECIMAL_SHA256_CHARACTERS"
    }
  ]
}
```

The launcher accepts HTTPS GitHub Release asset URLs and requires a 64-character SHA-256 digest.
It verifies the index digest against the downloaded bytes and checks the asset against GitHub Release metadata.
The plugin package must also carry a valid package signature. A self-signed certificate verifies package
integrity; it does not establish the author's real-world identity. Unsigned packages require explicit user
confirmation, and packages with invalid signatures are rejected.

Keep package metadata truthful, use stable plugin IDs, and update the version, release URL, and digest together.
