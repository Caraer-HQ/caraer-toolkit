# Page Trait Property Reference

Enabling the `page` trait provisions the CMS/page properties below. Object
templates should reference this document instead of duplicating the table.

## Trait configuration

| Field | Default |
| --- | --- |
| `name` | `page` |
| `rootSlug` | Workspace-defined |
| `generateRule` | `generate` |
| `publishRule` | `publishAlways` |

## Provisioned properties

| Name | Label (NL) | Label (EN) | Type | Format | Group | Options | Settings | Required when | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `environments` | Omgevingen | Environments | multi-select | multi-select | Website | Environment names | - | - | Publication visibility context. |
| `page_v2_staging` | Conceptinhoud | Draft Content | structure | structure | Website | — | - | - | Editable CMS content. |
| `page_v2_production` | Gepubliceerde inhoud | Published Content | structure | structure | Website | — | - | - | Served CMS content. |
| `page_v2_slug` | Slug | Slug | string | single-line | Website | — | - | - | URL-friendly page identifier. |
| `page_v2_title` | Titel | Title | string | single-line | Website | — | - | - | Canonical page title. |
| `page_v2_is_published` | Gepubliceerd | Is Published | checkbox | single-checkbox | Website | — | - | - | Publication state. |
| `page_v2_published_at` | Gepubliceerd op | Published At | date | date | Website | — | - | - | Publication timestamp. |
| `page_v2_publish_at` | Publiceren op | Publish At | date | date | Website | — | - | - | Optional scheduled publication. |
| `page_v2_unpublish_at` | Depubliceren op | Unpublish At | date | date | Website | — | - | - | Optional scheduled unpublication. |
| `page_v2_revision` | Revisie | Revision | number | number | Website | — | - | - | Monotonic CMS revision counter. |
| `page_v2_history` | Conceptgeschiedenis | Draft History | structure | structure | Website | — | - | - | Previous draft snapshots. |
