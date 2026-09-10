# Meta Campaign Object Template

Status: Central primary object.

## Purpose

`meta_campaign` represents a campaign imported from Meta Ads.

## Traits

### Enabled by default

- **Table** — campaign list.

### Optional by workspace configuration

- **Analytics** — campaign performance reporting.

### Not enabled by default

- Provider-specific write automation is not implied by this template.

## Core Properties

| Property | NL label | EN label | Meta type | Caraer type | Options / notes | Settings |
| --- | --- | --- | --- | --- | --- | --- |
| `campaign_id` | Campagne-ID | Campaign ID | string | `string` / `single-line` | Unique provider ID. | Required; unique |
| `campaign_name` | Campagnenaam | Campaign name | string | `tag` / `tag` | Preserve the provider text exactly; each distinct imported name becomes a tag option. | Optional |
| `account_id` | Account-ID | Account ID | string | `string` / `single-line` | Provider reference. | Optional |
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
| `objective` | Doelstelling | Objective | enum | `single-select` | See [Objective options](#objective-options). |
| `buying_type` | Inkooptype | Buying type | enum | `single-select` | See [Buying type options](#buying-type-options). |
| `unique_outbound_clicks` | Unieke uitgaande klikken | Unique outbound clicks | array<object> | `structure` / `structure` | Action type/value pairs. |
| `outbound_clicks` | Uitgaande klikken | Outbound clicks | array<object> | `structure` / `structure` | Action type/value pairs. |
| `cost_per_unique_outbound_click` | Kosten per unieke uitgaande klik | Cost per unique outbound click | array<object> | `structure` / `structure` | Action type/value pairs. |
| `cost_per_outbound_click` | Kosten per uitgaande klik | Cost per outbound click | array<object> | `structure` / `structure` | Action type/value pairs. |
| `post_engagement` | Postbetrokkenheid | Post engagement | integer | `number` / `number` | Count. |
| `post_reaction` | Postreacties | Post reactions | integer | `number` / `number` | Count. |
| `video_p100_watched_actions` | Video 100% bekeken acties | Video 100% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p25_watched_actions` | Video 25% bekeken acties | Video 25% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p50_watched_actions` | Video 50% bekeken acties | Video 50% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p75_watched_actions` | Video 75% bekeken acties | Video 75% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_p95_watched_actions` | Video 95% bekeken acties | Video 95% watched actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `video_play_actions` | Video-afspeelacties | Video play actions | array<object> | `structure` / `structure` | Action type/value pairs. |
| `date_start` | Startdatum | Start date | date | `date` / `date` | Reporting period start. | Required |
| `date_stop` | Einddatum | End date | date | `date` / `date` | Reporting period end. | Required |
| `insights_raw` | Ruwe inzichten | Raw insights | object | `structure` / `structure` | Complete provider response. |

## Direct Meta resource fields

The fields below complete the direct Meta `Campaign` resource surface. Meta field types are from the official generated SDK v26.0.1. The existing normalized reporting fields remain in **Core Properties**.

Existing aliases: `id` → `campaign_id`; `name` → `campaign_name`; `account_id` → `account_id`; `objective` → `objective`; `buying_type` → `buying_type`.

| Meta field | NL label | EN label | Meta type | Caraer type | Persistence rule |
| --- | --- | --- | --- | --- | --- |
| `adlabels` | Advertentielabels | Ad labels | `list<AdLabel>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `advantage_state_info` | Advantage-statusinformatie | Advantage state information | `AdCampaignGroupAdvantageState` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `bid_strategy` | Biedstrategie | Bid strategy | `BidStrategy` | `single-select` / `single-select` | Meta enum. [Bid strategy options](#bid-strategy-options). |
| `boosted_object_id` | ID gepromoot object | Boosted object ID | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `brand_lift_studies` | Merkeffectonderzoeken | Brand lift studies | `list<AdStudy>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `budget_rebalance_flag` | Budgetherverdeling | Budget rebalancing | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `budget_remaining` | Resterend budget | Remaining budget | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `campaign_group_active_time` | Actieve tijd campagnegroep | Campaign group active time | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `can_create_brand_lift_study` | Merkeffectonderzoek mogelijk | Can create brand lift study | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `can_use_spend_cap` | Uitgavenlimiet mogelijk | Can use spend cap | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `configured_status` | Ingestelde status | Configured status | `ConfiguredStatus` | `single-select` / `single-select` | Meta enum. [Configured status options](#configured-status-options). |
| `created_time` | Aangemaakt op | Created time | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `daily_budget` | Dagbudget | Daily budget | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `effective_status` | Effectieve status | Effective status | `EffectiveStatus` | `single-select` / `single-select` | Meta enum. [Effective status options](#effective-status-options). |
| `frequency_control_specs` | Frequentiebeheerspecificaties | Frequency control specifications | `list<AdCampaignFrequencyControlSpecs>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `has_secondary_skadnetwork_reporting` | Secundaire SKAdNetwork-rapportage | Secondary SKAdNetwork reporting | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_adset_budget_sharing_enabled` | Budgetdeling tussen advertentiesets ingeschakeld | Ad set budget sharing enabled | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_budget_schedule_enabled` | Budgetplanning ingeschakeld | Budget scheduling enabled | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_direct_send_campaign` | Direct Send-campagne | Direct Send campaign | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_message_campaign` | Berichtencampagne | Message campaign | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_meta_moment_maker_enabled` | Meta Moment Maker ingeschakeld | Meta Moment Maker enabled | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_reels_trending_ads_enabled` | Reels Trending Ads ingeschakeld | Reels Trending Ads enabled | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_skadnetwork_attribution` | SKAdNetwork-attributie | SKAdNetwork attribution | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `issues_info` | Probleeminformatie | Issue information | `list<AdCampaignIssuesInfo>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `last_budget_toggling_time` | Laatste budgetomschakeling | Last budget toggling time | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `lifetime_budget` | Looptijdbudget | Lifetime budget | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `pacing_type` | Budgetspreidingstypen | Pacing types | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `primary_attribution` | Primaire attributie | Primary attribution | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `promoted_object` | Gepromoot object | Promoted object | `AdPromotedObject` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `recommendations` | Aanbevelingen | Recommendations | `list<AdRecommendation>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `smart_promotion_type` | Slim promotietype | Smart promotion type | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `source_campaign` | Broncampagnegegevens | Source campaign data | `Campaign` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `source_campaign_id` | Broncampagne-ID | Source campaign ID | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `source_recommendation_type` | Type bronaanbeveling | Source recommendation type | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `special_ad_categories` | Speciale advertentiecategorieën | Special ad categories | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `special_ad_category` | Speciale advertentiecategorie | Special ad category | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `special_ad_category_country` | Landen speciale advertentiecategorie | Special ad category countries | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `spend_cap` | Uitgavenlimiet | Spend cap | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `start_time` | Starttijd | Start time | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `status` | Status | Status | `Status` | `single-select` / `single-select` | Meta enum. [Configured status options](#configured-status-options). |
| `stop_time` | Eindtijd campagne | Campaign stop time | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `topline_id` | Topline-ID | Topline ID | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `updated_time` | Bijgewerkt op | Updated time | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `adbatch` | Advertentiebatch | Ad batch | `list<Object>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `budget_schedule_specs` | Budgetplanningsspecificaties | Budget schedule specifications | `list<Object>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `execution_options` | Uitvoeringsopties | Execution options | `list<ExecutionOptions>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `iterative_split_test_configs` | Iteratieve splittestconfiguraties | Iterative split test configurations | `list<Object>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |


## Objective options

Use current `OUTCOME_*` values for new campaigns. The compatibility values are
included for importing historical provider data; enable them only when a portal
needs to preserve or accept those values.

**Visual treatment:** Large neutral — 21 provider objectives; all use a soft gray background and no icon.

| Value | NL label | EN label | Use | Color | Icon |
| --- | --- | --- | --- | --- | --- |
| `OUTCOME_AWARENESS` | Bekendheid | Awareness | Current | `#F3F4F6` | `—` |
| `OUTCOME_TRAFFIC` | Verkeer | Traffic | Current | `#F3F4F6` | `—` |
| `OUTCOME_ENGAGEMENT` | Betrokkenheid | Engagement | Current | `#F3F4F6` | `—` |
| `OUTCOME_LEADS` | Leads | Leads | Current | `#F3F4F6` | `—` |
| `OUTCOME_APP_PROMOTION` | App-promotie | App promotion | Current | `#F3F4F6` | `—` |
| `OUTCOME_SALES` | Verkopen | Sales | Current | `#F3F4F6` | `—` |
| `APP_INSTALLS` | App-installaties | App installs | Compatibility | `#F3F4F6` | `—` |
| `BRAND_AWARENESS` | Merkbekendheid | Brand awareness | Compatibility | `#F3F4F6` | `—` |
| `CONVERSIONS` | Conversies | Conversions | Compatibility | `#F3F4F6` | `—` |
| `EVENT_RESPONSES` | Evenementreacties | Event responses | Compatibility | `#F3F4F6` | `—` |
| `LEAD_GENERATION` | Leadgeneratie | Lead generation | Compatibility | `#F3F4F6` | `—` |
| `LINK_CLICKS` | Linkklikken | Link clicks | Compatibility | `#F3F4F6` | `—` |
| `LOCAL_AWARENESS` | Lokale bekendheid | Local awareness | Compatibility | `#F3F4F6` | `—` |
| `MESSAGES` | Berichten | Messages | Compatibility | `#F3F4F6` | `—` |
| `OFFER_CLAIMS` | Aanbiedingen claimen | Offer claims | Compatibility | `#F3F4F6` | `—` |
| `PAGE_LIKES` | Pagina-likes | Page likes | Compatibility | `#F3F4F6` | `—` |
| `POST_ENGAGEMENT` | Berichtbetrokkenheid | Post engagement | Compatibility | `#F3F4F6` | `—` |
| `PRODUCT_CATALOG_SALES` | Productcatalogusverkopen | Product catalog sales | Compatibility | `#F3F4F6` | `—` |
| `REACH` | Bereik | Reach | Compatibility | `#F3F4F6` | `—` |
| `STORE_VISITS` | Winkelbezoeken | Store visits | Compatibility | `#F3F4F6` | `—` |
| `VIDEO_VIEWS` | Videoweergaven | Video views | Compatibility | `#F3F4F6` | `—` |

## Buying type options

Use Meta provider values exactly as uppercase identifiers. Store the provider
value separately from its display labels.

**Visual treatment:** Small categorical — 2 values; use distinct soft colours and no icons.

| Value | NL label | EN label | Color | Icon |
| --- | --- | --- | --- | --- |
| `AUCTION` | Veiling | Auction | `#DBEAFE` | `—` |
| `RESERVED` | Gereserveerd | Reserved | `#EDE9FE` | `—` |

## Bid strategy options

**Visual treatment:** Small categorical — 4 values; use distinct soft colours and no icons.

| Value | NL label | EN label | Color | Icon |
| --- | --- | --- | --- | --- |
| `COST_CAP` | Kostenlimiet | Cost cap | `#E0F2FE` | `—` |
| `LOWEST_COST_WITHOUT_CAP` | Laagste kosten zonder limiet | Lowest cost without cap | `#DCFCE7` | `—` |
| `LOWEST_COST_WITH_BID_CAP` | Laagste kosten met biedlimiet | Lowest cost with bid cap | `#FEF3C7` | `—` |
| `LOWEST_COST_WITH_MIN_ROAS` | Laagste kosten met minimale ROAS | Lowest cost with minimum ROAS | `#FCE7F3` | `—` |

## Configured status options

**Visual treatment:** Semantic state — use status colours and icons.

| Value | NL label | EN label | Color | Icon |
| --- | --- | --- | --- | --- |
| `ACTIVE` | Actief | Active | `#DCFCE7` | `checkCircle` |
| `ARCHIVED` | Gearchiveerd | Archived | `#F3F4F6` | `archive` |
| `DELETED` | Verwijderd | Deleted | `#FEE2E2` | `trash2` |
| `PAUSED` | Gepauzeerd | Paused | `#FEF3C7` | `pauseCircle` |

## Effective status options

One shared `effective_status` property (`single-select` / `single-select`) is
attached to Campaign, Ad Set, and Ad within each adopting portal. Maintain the
complete 12-option union below once; do not create object-specific copies or
replace the shared options with a smaller subset when provisioning an object.
This is a shared definition, not a shared record value: each record retains its
own effective status.

**Visual treatment:** Semantic state — preserve the shared labels, soft colours,
and icon choices. Verify icon identifiers before applying them to a portal.

**Applicability:** The last column preserves the object-level sets previously
documented in these templates. All three dropdowns expose the union; integrations
must respect the provider-level applicability rather than treating every option
as valid for every Meta object. Do not globally disable an option merely because
it does not apply to Campaign or Ad Set.

`Value` is the exact Meta provider value. Where Caraer requires lowercase option
`name`s, map explicitly (for example, `ACTIVE` ↔ `active`) and preserve existing
stored keys. This template change does not migrate records or importers.

| Value | NL label | EN label | Color | Icon | Provider-level applicability |
| --- | --- | --- | --- | --- | --- |
| `ACTIVE` | Actief | Active | `#DCFCE7` | `checkCircle` | Campaign, Ad Set, Ad |
| `ADSET_PAUSED` | Ad set gepauzeerd | Ad set paused | `#FEF3C7` | `pauseCircle` | Ad |
| `ARCHIVED` | Gearchiveerd | Archived | `#F3F4F6` | `archive` | Campaign, Ad Set, Ad |
| `CAMPAIGN_PAUSED` | Campagne gepauzeerd | Campaign paused | `#FEF3C7` | `pauseCircle` | Ad Set, Ad |
| `DELETED` | Verwijderd | Deleted | `#FEE2E2` | `trash2` | Campaign, Ad Set, Ad |
| `DISAPPROVED` | Afgekeurd | Disapproved | `#FEE2E2` | `xCircle` | Ad |
| `IN_PROCESS` | In behandeling | In process | `#DBEAFE` | `loaderCircle` | Campaign, Ad Set, Ad |
| `PAUSED` | Gepauzeerd | Paused | `#FEF3C7` | `pauseCircle` | Campaign, Ad Set, Ad |
| `PENDING_BILLING_INFO` | Factuurgegevens in afwachting | Pending billing info | `#FEF3C7` | `clock3` | Ad |
| `PENDING_REVIEW` | Beoordeling in afwachting | Pending review | `#FEF3C7` | `clock3` | Ad |
| `PREAPPROVED` | Vooraf goedgekeurd | Preapproved | `#DBEAFE` | `badgeCheck` | Ad |
| `WITH_ISSUES` | Met problemen | With issues | `#FEE2E2` | `triangleAlert` | Campaign, Ad Set, Ad |

## Relations

- `conversion` ↔ `Candidate` (`candidate`), label **Conversie**. Reuse one shared relation definition across Campaign, Ad Set, and Ad. It links a candidate to each explicitly attributed Meta record; schema creation does not create record links or infer attribution from the parent hierarchy.

- `campaign_ad_sets` → `Meta Ad Set`.
