# Meta Ad Object Template

Status: Central primary object.

## Purpose

`meta_ad` represents an individual Meta advertisement and its performance
insights for a reporting period.

## Traits

### Enabled by default

- **Table** — ad performance list.

### Optional by workspace configuration

- **Analytics** — ad-level performance reporting.

### Not enabled by default

- Provider-specific write automation is not implied by this template.

## Core Properties

| Property | NL label | EN label | Meta type | Caraer type | Options / notes | Settings |
| --- | --- | --- | --- | --- | --- | --- |
| `ad_id` | Advertentie-ID | Ad ID | string | `string` / `single-line` | Unique provider ID. | Required; unique |
| `adset_id` | Adset-ID | Ad set ID | string | `linked-property` | Linked to Meta Ad Set; system-managed. | Linked property |
| `adset_name` | Adsetnaam | Ad set name | string | `linked-property` | Linked to Meta Ad Set; system-managed. | Linked property |
| `campaign_id` | Campagne-ID | Campaign ID | string | `linked-property` | Linked through Meta Ad Set; system-managed. | Linked property |
| `campaign_name` | Campagnenaam | Campaign name | string | `linked-property` | Linked through Meta Ad Set; system-managed. | Linked property |
| `account_id` | Account-ID | Account ID | string | `string` / `single-line` | Provider reference. | Optional |
| `ad_name` | Advertentienaam | Ad name | string | `tag` / `tag` | Preserve the provider text exactly; each distinct imported name becomes a tag option. |
| `spend` | Uitgaven | Spend | decimal | `number` / `currency` | Monetary value. |
| `social_spend` | Sociale uitgaven | Social spend | decimal | `number` / `currency` | Monetary value. |
| `leads` | Leads | Leads | integer | `number` / `number` | Count. |
| `impressions` | Vertoningen | Impressions | integer | `number` / `number` | Count. |
| `reach` | Bereik | Reach | integer | `number` / `number` | Count. |
| `frequency` | Frequentie | Frequency | decimal | `number` / `number` | Average impressions per reached person. |
| `clicks` | Klikken | Clicks | integer | `number` / `number` | Count. |
| `unique_clicks` | Unieke klikken | Unique clicks | integer | `number` / `number` | Count. |
| `inline_link_clicks` | Inline linkklikken | Inline link clicks | integer | `number` / `number` | Count. |
| `unique_inline_link_clicks` | Unieke inline linkklikken | Unique inline link clicks | integer | `number` / `number` | Count. |
| `actions` | Acties | Actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `action_values` | Actiewaarden | Action values | array<object> | `structure` / `structure` | Value pairs by action type. |
| `conversions` | Conversies | Conversions | array<object> | `structure` / `structure` | Conversion data. |
| `cpc` | Kosten per klik | Cost per click | decimal | `number` / `currency` | Monetary value. |
| `cpm` | Kosten per duizend vertoningen | Cost per mille | decimal | `number` / `currency` | Monetary value. |
| `ctr` | Klikfrequentie | Click-through rate | decimal | `number` / `number` | Percentage value. |
| `unique_ctr` | Unieke klikfrequentie | Unique click-through rate | decimal | `number` / `number` | Percentage value. |
| `cost_per_inline_link_click` | Kosten per inline linkklik | Cost per inline link click | decimal | `number` / `currency` | Monetary value. |
| `cost_per_unique_inline_link_click` | Kosten per unieke inline linkklik | Cost per unique inline link click | decimal | `number` / `currency` | Monetary value. |
| `cost_per_action_type` | Kosten per actietype | Cost per action type | array<object> | `structure` / `structure` | Action type/value pairs. |
| `cost_per_conversion` | Kosten per conversie | Cost per conversion | decimal | `number` / `currency` | Conversion cost. |
| `unique_outbound_clicks` | Unieke uitgaande klikken | Unique outbound clicks | array<object> | `structure` / `structure` | Action type/value pairs. |
| `outbound_clicks` | Uitgaande klikken | Outbound clicks | array<object> | `structure` / `structure` | Action type/value pairs. |
| `cost_per_unique_outbound_click` | Kosten per unieke uitgaande klik | Cost per unique outbound click | array<object> | `structure` / `structure` | Action type/value pairs. |
| `cost_per_outbound_click` | Kosten per uitgaande klik | Cost per outbound click | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p100_watched_actions` | Video 100% bekeken acties | Video 100% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p25_watched_actions` | Video 25% bekeken acties | Video 25% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p50_watched_actions` | Video 50% bekeken acties | Video 50% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p75_watched_actions` | Video 75% bekeken acties | Video 75% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p95_watched_actions` | Video 95% bekeken acties | Video 95% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_play_actions` | Video-afspeelacties | Video play actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `post_engagement` | Postbetrokkenheid | Post engagement | integer | `number` / `number` | Count. |
| `post_reaction` | Postreacties | Post reactions | integer | `number` / `number` | Count. |
| `objective` | Doelstelling | Objective | enum | `single-select` | See [Meta Campaign objective options](meta-campaign.md#objective-options). |
| `buying_type` | Inkooptype | Buying type | enum | `single-select` | See [Meta Campaign buying-type options](meta-campaign.md#buying-type-options). |
| `date_start` | Startdatum | Start date | date | `date` / `date` | Reporting period start. | Required |
| `date_stop` | Einddatum | End date | date | `date` / `date` | Reporting period end. | Required |
| `insights_raw` | Ruwe inzichten | Raw insights | object | `structure` / `structure` | Complete provider response. |

## Direct Meta resource fields

The fields below complete the direct Meta `Ad` resource surface. Meta field types are from the official generated SDK v26.0.1. The existing normalized reporting fields remain in **Core Properties**.

Existing aliases: `id` → `ad_id`; `name` → `ad_name`; `account_id` → `account_id`; `adset_id` and `campaign_id` → linked properties.

| Meta field | Meta type | Caraer type | Persistence rule |
| --- | --- | --- | --- |
| `ad_active_time` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `ad_review_feedback` | `AdgroupReviewFeedback` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `ad_schedule_end_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `ad_schedule_start_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `adlabels` | `list<AdLabel>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `adset` | `AdSet` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `bid_amount` | `int` | `number` / `number` | Provider numeric scalar. |
| `bid_info` | `map<string, unsigned int>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `bid_type` | `BidType` | `single-select` / `single-select` | Meta enum. [Bid-type options](#bid-type-options). |
| `campaign` | `Campaign` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `configured_status` | `ConfiguredStatus` | `single-select` / `single-select` | Meta enum. [Configured status options](meta-campaign.md#configured-status-options). |
| `conversion_domain` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `conversion_specs` | `list<ConversionActionQuery>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `created_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `creative` | `AdCreative` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `creative_asset_groups_spec` | `AdCreativeAssetGroupsSpec` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `creative_automation_spec` | `AdCreativeAutomationSpec` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `demolink_hash` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `display_sequence` | `int` | `number` / `number` | Provider numeric scalar. |
| `effective_status` | `EffectiveStatus` | `single-select` / `single-select` | Meta enum. [Shared effective-status options](meta-campaign.md#effective-status-options). |
| `engagement_audience` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `failed_delivery_checks` | `list<DeliveryCheck>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `issues_info` | `list<AdgroupIssuesInfo>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `last_updated_by_app_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `placement` | `Placement` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `preview_shareable_link` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `priority` | `unsigned int` | `number` / `number` | Store as Caraer `meta_priority` (label: Meta-prioriteit). Map Meta `priority` ↔ Caraer `meta_priority`; preserve the existing shared `priority` dropdown. Preserve unsigned integer semantics in the integration. |
| `recommendations` | `list<AdRecommendation>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `source_ad` | `Ad` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `source_ad_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `special_ad_categories` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `status` | `Status` | `single-select` / `single-select` | Meta enum. [Configured status options](meta-campaign.md#configured-status-options). |
| `targeting` | `Targeting` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `tracking_and_conversion_with_defaults` | `TrackingAndConversionWithDefaults` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `tracking_specs` | `list<ConversionActionQuery>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `updated_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `adset_spec` | `AdSet` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `audience_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `dataset_split_specs` | `list<map>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `date_format` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `draft_adgroup_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `execution_options` | `list<ExecutionOptions>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `include_demolink_hashes` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `filename` | `file` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |

## Bid-type options

**Visual treatment:** Small categorical — 5 values; use distinct soft colours and no icons.

| Value | NL label | EN label | Color | Icon |
| --- | --- | --- | --- | --- |
| `ABSOLUTE_OCPM` | Absolute OCPM | Absolute OCPM | `#DBEAFE` | `—` |
| `CPA` | Kosten per actie | Cost per action | `#DCFCE7` | `—` |
| `CPC` | Kosten per klik | Cost per click | `#FEF3C7` | `—` |
| `CPM` | Kosten per duizend vertoningen | Cost per mille | `#FCE7F3` | `—` |
| `MULTI_PREMIUM` | Meervoudige premie | Multi premium | `#EDE9FE` | `—` |

## Effective-status options

Reuse the single shared [`effective_status` property and complete 12-option set](meta-campaign.md#effective-status-options)
attached to Campaign, Ad Set, and Ad. Labels, colours, icons, and provider-level
applicability are maintained there; do not provision a separate subset for this object.

## Raw insight structure

`insights_raw` may contain:

```json
{
  "spend": "66.17",
  "impressions": "2021",
  "clicks": "15",
  "actions": [
    {
      "action_type": "link_click",
      "value": "10"
    }
  ],
  "campaign_id": "120223032198970582",
  "adset_id": "120226658694920582",
  "date_start": "2025-01-01",
  "date_stop": "2025-12-31"
}
```

The `actions` array is preserved as provider data. Normalized action metrics
may be added later if reporting needs stable fields for them.

## Relations

- `conversion` ↔ `Candidate` (`candidate`), label **Conversie**. Reuse one shared relation definition across Campaign, Ad Set, and Ad. It links a candidate to each explicitly attributed Meta record; schema creation does not create record links or infer attribution from the parent hierarchy.

- `ad_ad_set` → `Meta Ad Set`.
- `ad_campaign` → `Meta Campaign` when the provider reference is available.

`adset_id`, `adset_name`, `campaign_id`, and `campaign_name` are linked
properties. Their canonical values come from the related Meta Ad Set and Meta
Campaign records, not from independent Ad fields.
