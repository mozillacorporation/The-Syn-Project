# The Syn Project - Public version

## Overview

The public version automatically scans `ReplicatedStorage` for path references and generates the corresponding instance hierarchy.

For example, the following path:

```lua
serverscriptservice.a.b
```

will generate the following structure:

```text
ServerScriptService
└── a
    └── b (ModuleScript)
```

## How It Works

1. Scans `ReplicatedStorage` for dot-separated path references.
2. Parses the path into its hierarchical structure.
3. Creates any missing `Folder` instances for intermediate path segments.
4. Creates a `ModuleScript` with the name of the final path segment.
5. Places the generated hierarchy in the appropriate Roblox service (e.g. `ServerScriptService` `ServerStorage`).

## Example

### Input

```lua
serverscriptservice.a.b
```

### Output

```text
ServerScriptService
└── a
    └── b (ModuleScript)
```

## Notes

- Intermediate path segments are created as `Folder` instances.
- The final path segment is always created as a `ModuleScript`.
- Existing folders and modules are reused when possible instead of being recreated.
- Paths are case-insensitive when resolving Roblox services (e.g. `serverscriptservice` → `ServerScriptService`).
- THIS IS NOT AN EXPLOIT TOOL!
