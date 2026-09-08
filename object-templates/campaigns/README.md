# Campaigns Suite

Central suite for campaign structures and advertising performance data.

## Object hierarchy

```text
Meta Campaign
└── Meta Ad Set
    └── Meta Ad
```

The suite stores normalized reporting fields together with provider-specific
raw insight data for traceability.

## Caraer type mapping

The mapping below follows the live Caraer MCP schema helpers:

| Meta type | Caraer type | Caraer format |
| --- | --- | --- |
| string | `string` | `single-line` |
| enum | `single-select` | `single-select` |
| integer | `number` | `number` |
| decimal | `number` | `number` or `currency` |
| date | `date` | `date` |
| datetime | `string` | `single-line` (ISO 8601 timestamp) |
| boolean | `checkbox` | `single-checkbox` |
| object / array | `structure` | `structure` |

Use `structure` for provider-defined objects, maps, lists, and file descriptors
unless a stable, separately modelled Caraer object exists. This preserves the
complete Meta payload rather than flattening or discarding provider fields.

Caraer currently exposes a date format but no verified datetime format. Store
Meta timestamps as ISO 8601 `string` values until a datetime format is
available, so their time and timezone are not lost.

## Select-option presentation

Every documented `single-select`, `multi-select`, or `tag` option may define
`name`, `label`, `color`, `icon`, and `disabled`. The provider `name` remains
the stored/imported value; visual metadata must never change it.

| Option family | Rule | Colour and icon treatment |
| --- | --- | --- |
| Semantic state | Values communicate a positive, negative, pending, paused, or archived state. | Use soft green/red/amber/gray/blue colours and a meaningful state icon. |
| Small categorical | 1–12 values without a positive/negative meaning. | Use a distinct soft colour per value; leave icons empty unless the value has an obvious, stable icon. |
| Large categorical | 13 or more values without a positive/negative meaning. | Use soft gray (`#F3F4F6`) for every value and no icon, to avoid visual noise. |

The option tables state their chosen treatment and include the exact `color`
and `icon` values to provision. An em dash (`—`) means omit that optional
field. The library uses CSS hex colours and Caraer icon-picker identifiers;
verify an icon exists in the target portal before a live schema write.

## Shared effective status

Adopt one `effective_status` property across Meta Campaign, Meta Ad Set, and Meta
Ad, with the [canonical 12-option union](meta-campaign.md#effective-status-options).
Reuse the same property definition and presentation metadata on all three objects;
each record stores its own value. Provider-level applicability is documented in
the canonical table, not enforced by splitting the shared dropdown into subsets.

## Property settings

The provider identifiers use Meta's exact field names:

| Property | Setting | Reason |
| --- | --- | --- |
| `campaign_id` on Meta Campaign | Required; unique | Primary campaign identifier. |
| `adset_id` on Meta Ad Set | Required; unique | Primary ad-set identifier. |
| `ad_id` on Meta Ad | Required; unique | Primary ad identifier. |
| Parent IDs on child objects | Required or linked property | Parent links should resolve through the object hierarchy. |
| `account_id` | Optional | Account context may be unavailable in some provider responses. |
| `campaign_name`, `adset_name`, `ad_name` | Optional tag | Keep the exact imported name; a distinct source value creates a reusable tag option. |

Meta calls the ad-set identifier `adset_id`; the English label remains **Ad
Set ID**, while the stored property name follows Meta exactly.

## Linked-property review

| Object | Linked properties | Source |
| --- | --- | --- |
| Meta Campaign | None currently | `campaign_id` is the primary unique identifier. `account_id` remains optional because no Meta Ad Account object exists yet. |
| Meta Ad Set | `campaign_id`, `campaign_name` | Related Meta Campaign. |
| Meta Ad | `adset_id`, `adset_name` | Related Meta Ad Set. |
| Meta Ad | `campaign_id`, `campaign_name` | Related Meta Campaign through the Ad Set. |

Linked properties are system-managed and should not be maintained as
independent child-object values.

MCP verification performed against the Caraer Main endpoint:

- `property_types_list` returned `string`, `single-select`, `multi-select`,
  `date`, `number`, `structure`, and related system types.
- `property_formats_list` returned `single-line`, `single-select`, `number`,
  `currency`, `date`, and `structure` formats.
- `property_value_shapes_list` confirmed JSON/object values for `structure`
  and option values for `single-select`.
- `object_list(query: "Meta")` returned no existing live Meta objects, so
  campaign-specific Caraer property options do not exist yet. Options shown in
  the object templates are therefore provider values or values from the
  supplied payload and still need to be created when the live objects are
  provisioned.
