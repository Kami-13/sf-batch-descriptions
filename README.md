# Managed batch descriptions

`managed-batches.json` provides descriptions for Salesforce managed-package batch classes (Consumer Goods Cloud). Salesforce strips the doc comments from managed code, so a tool listing an org's batches can't read these descriptions from the org. This file fills the gap. The SBX Batch Runner browser extension reads it from:

```
https://raw.githubusercontent.com/Kami-13/sbx-batch-descriptions/main/managed-batches.json
```

Your own (unmanaged) batches don't belong here. Their descriptions come from the class's doc comment (`@description`).

## Format

Each key is the class's API name, `namespace.ClassName`.

| Field | Required | Meaning |
| --- | --- | --- |
| `description` | yes (`null` if unknown) | One or two sentences on what the batch does. |
| `source` | yes (`null` if unknown) | The page the description comes from. |
| `verified` | yes | `true` once someone has checked the description against the source. |
| `batchSize` | no | Recommended batch size, when the vendor gives one. |
| `configName` | no | The CG Cloud Batch Process Configuration name, when it differs from the class. |
| `notes` | no | Caveats: prerequisites, ordering, scheduling limits. |

## Coverage

- **cgcloud:** all 21 global batch classes in package version 260.2 are listed. 12 are described from Salesforce docs. 9 have no public documentation yet (`description: null`).
- **maps:** none. Salesforce Maps has no global batch classes, so none of its batches can be started from outside the package.

## Adding or fixing an entry

- Only write what a source says. Leave `description` null rather than guessing from the class name.
- Set `verified: true` after reading the source page yourself.
- Update `updated` at the top of the file.
