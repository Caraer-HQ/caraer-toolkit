# System Property Reference

These properties are provisioned by Caraer on objects. Object templates should
reference this document instead of repeating the system-property table.

They are normally not created manually through MCP.

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `uuid` | UUID | UUID | string | single-line | System | — | Unique | - | Immutable unique record identifier. |
| `createdAt` | Aangemaakt op | Created At | date | date | System | — | - | - | Immutable creation timestamp. |
| `updatedAt` | Bijgewerkt op | Updated At | date | date | System | — | - | - | Immutable system timestamp. |
| `deletedAt` | Verwijderd op | Deleted At | date | date | System | — | - | - | Soft-delete timestamp; system-managed. |
| `primary_object` | Primair object | Primary Object | single-select | single-select | System | Object names | - | - | System ownership context. |
| `extended_objects` | Morph-objecten | Morph Objects | multi-select | multi-select | System | Object names | - | - | System extension context. |

The exact system options for `primary_object` and `extended_objects` are
portal-managed and may grow as objects are added.
