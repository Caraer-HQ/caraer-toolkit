# Meta Ad Set Object Template

Status: Central primary object.

## Purpose

`meta_ad_set` represents an ad set imported from Meta Ads.

## Traits

### Enabled by default

- **Table** — ad-set list.

### Optional by workspace configuration

- **Analytics** — ad-set performance reporting.

### Not enabled by default

- Provider-specific write automation is not implied by this template.

## Core Properties

| Property | NL label | EN label | Meta type | Caraer type | Options / notes | Settings |
| --- | --- | --- | --- | --- | --- | --- |
| `adset_id` | Adset-ID | Ad set ID | string | `string` / `single-line` | Unique provider ID. | Required; unique |
| `adset_name` | Adsetnaam | Ad set name | string | `tag` / `tag` | Preserve the provider text exactly; each distinct imported name becomes a tag option. |
| `campaign_id` | Campagne-ID | Campaign ID | string | `linked-property` | Linked to Meta Campaign; system-managed. | Linked property |
| `campaign_name` | Campagnenaam | Campaign name | string | `linked-property` | Linked to Meta Campaign; system-managed. | Linked property |
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
| `objective` | Doelstelling | Objective | enum | `single-select` | See [Meta Campaign objective options](meta-campaign.md#objective-options). |
| `buying_type` | Inkooptype | Buying type | enum | `single-select` | See [Meta Campaign buying-type options](meta-campaign.md#buying-type-options). |
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
| `date_start` | Startdatum | Start date | date | `date` / `date` | Reporting period start. | Required |
| `date_stop` | Einddatum | End date | date | `date` / `date` | Reporting period end. | Required |
| `insights_raw` | Ruwe inzichten | Raw insights | object | `structure` / `structure` | Complete provider response. |

## Direct Meta resource fields

The fields below complete the direct Meta `AdSet` resource surface. Meta field types are from the official generated SDK v26.0.1. The existing normalized reporting fields remain in **Core Properties**.

Existing aliases: `id` → `adset_id`; `name` → `adset_name`; `account_id` → `account_id`; `campaign_id` → linked `campaign_id`.

| Meta field | Meta type | Caraer type | Persistence rule |
| --- | --- | --- | --- |
| `ad_set_goal` | `AdCampaignGoal` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `adlabels` | `list<AdLabel>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `adset_schedule` | `list<DayPart>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `anchor_event_attribution_window_days` | `int` | `number` / `number` | Provider numeric scalar. |
| `asset_feed_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `attribution_count_type` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `attribution_spec` | `list<AttributionSpec>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `automatic_manual_state` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `bid_adjustments` | `AdBidAdjustments` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `bid_amount` | `unsigned int` | `number` / `number` | Provider numeric scalar. |
| `bid_constraints` | `AdCampaignBidConstraint` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `bid_info` | `map<string, unsigned int>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `bid_strategy` | `BidStrategy` | `single-select` / `single-select` | Meta enum. [Bid strategy options](meta-campaign.md#bid-strategy-options). |
| `billing_event` | `BillingEvent` | `single-select` / `single-select` | Meta enum. [Billing event options](#billing-event-options). |
| `brand_safety_config` | `BrandSafetyCampaignConfig` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `budget_remaining` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `campaign` | `Campaign` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `campaign_active_time` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `campaign_attribution` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `configured_status` | `ConfiguredStatus` | `single-select` / `single-select` | Meta enum. [Configured status options](meta-campaign.md#configured-status-options). |
| `cost_bidding_mode` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `created_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `creative_diversity_label` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `creative_diversity_score` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `creative_sequence` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `creative_sequence_repetition_pattern` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `daily_budget` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `daily_min_spend_target` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `daily_spend_cap` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `destination_type` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `dsa_beneficiary` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `dsa_payor` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `effective_status` | `EffectiveStatus` | `single-select` / `single-select` | Meta enum. [Shared effective-status options](meta-campaign.md#effective-status-options). |
| `end_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `existing_customer_budget_percentage` | `unsigned int` | `number` / `number` | Provider numeric scalar. |
| `frequency_control_specs` | `list<AdCampaignFrequencyControlSpecs>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `full_funnel_exploration_mode` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `instagram_user_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `is_ba_skip_delayed_eligible` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_budget_schedule_enabled` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_dc_follow_optimized` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_dynamic_creative` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_incremental_attribution_enabled` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_organic_ad_joint_optimized` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `is_sequenced_conversion_creation` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `issues_info` | `list<AdCampaignIssuesInfo>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `learning_stage_info` | `AdCampaignLearningStageInfo` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `lifetime_budget` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `lifetime_imps` | `int` | `number` / `number` | Provider numeric scalar. |
| `lifetime_min_spend_target` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `lifetime_spend_cap` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `live_video_ad_campaign_config` | `LiveVideoAdCampaignConfig` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `low_creative_reach` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `max_budget_spend_percentage` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `meta_moment_maker_spec` | `MetaMomentMakerConfig` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `min_budget_spend_percentage` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `multi_event_conversion_attribution_window_seconds` | `int` | `number` / `number` | Provider numeric scalar. |
| `multi_optimization_goal_weight` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `optimization_goal` | `OptimizationGoal` | `single-select` / `single-select` | Meta enum. [Optimization-goal options](#optimization-goal-options). |
| `optimization_sub_event` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `pacing_type` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `placement_soft_opt_out` | `PlacementSoftOptOut` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `promoted_object` | `AdPromotedObject` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `recommendations` | `list<AdRecommendation>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `recurring_budget_semantics` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `regional_regulated_categories` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `regional_regulation_identities` | `RegionalRegulationIdentities` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `relative_value` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `review_feedback` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `rf_prediction_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `source_adset` | `AdSet` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `source_adset_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `special_ad_categories` | `list<string>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `start_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `status` | `Status` | `single-select` / `single-select` | Meta enum. [Configured status options](meta-campaign.md#configured-status-options). |
| `targeting` | `Targeting` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `targeting_optimization_types` | `list<map<string, int>>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `time_based_ad_rotation_id_blocks` | `list<list<int>>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `time_based_ad_rotation_intervals` | `list<unsigned int>` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `trending_topics_spec` | `TrendingTopicsSpec` | `structure` / `structure` | Provider structured value; preserve the complete JSON payload. |
| `updated_time` | `datetime` | `string` / `single-line` | ISO 8601 timestamp; keep as text because Caraer currently exposes a date, not datetime, format. |
| `use_new_app_click` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |
| `value_rule_set_id` | `string` | `string` / `single-line` | Provider string scalar; do not coerce it. |
| `value_rules_applied` | `bool` | `checkbox` / `single-checkbox` | Provider boolean; store the true/false value. |

## Billing event options

**Visual treatment:** Small categorical — 11 values; use distinct soft colours and no icons.

| Value | NL label | EN label | Color | Icon |
| --- | --- | --- | --- | --- |
| `APP_INSTALLS` | App-installaties | App installs | `#DBEAFE` | `—` |
| `CLICKS` | Klikken | Clicks | `#DCFCE7` | `—` |
| `IMPRESSIONS` | Vertoningen | Impressions | `#FEF3C7` | `—` |
| `LINK_CLICKS` | Linkklikken | Link clicks | `#FCE7F3` | `—` |
| `LISTING_INTERACTION` | Advertentie-interactie | Listing interaction | `#EDE9FE` | `—` |
| `NONE` | Geen | None | `#DBEAFE` | `—` |
| `OFFER_CLAIMS` | Aanbiedingen claimen | Offer claims | `#DCFCE7` | `—` |
| `PAGE_LIKES` | Pagina-likes | Page likes | `#FEF3C7` | `—` |
| `POST_ENGAGEMENT` | Berichtbetrokkenheid | Post engagement | `#FCE7F3` | `—` |
| `PURCHASE` | Aankoop | Purchase | `#EDE9FE` | `—` |
| `THRUPLAY` | ThruPlay | ThruPlay | `#DBEAFE` | `—` |

## Optimization-goal options

**Visual treatment:** Large neutral — 33 provider goals; all use a soft gray background and no icon.

| Value | NL label | EN label | Color | Icon |
| --- | --- | --- | --- | --- |
| `ADVERTISER_SILOED_VALUE` | Waarde per adverteerder | Advertiser siloed value | `#F3F4F6` | `—` |
| `AD_RECALL_LIFT` | Toename advertentieherinnering | Ad recall lift | `#F3F4F6` | `—` |
| `APP_INSTALLS` | App-installaties | App installs | `#F3F4F6` | `—` |
| `APP_INSTALLS_AND_OFFSITE_CONVERSIONS` | App-installaties en externe conversies | App installs and offsite conversions | `#F3F4F6` | `—` |
| `AUTOMATIC_OBJECTIVE` | Automatische doelstelling | Automatic objective | `#F3F4F6` | `—` |
| `CONVERSATIONS` | Gesprekken | Conversations | `#F3F4F6` | `—` |
| `DERIVED_EVENTS` | Afgeleide gebeurtenissen | Derived events | `#F3F4F6` | `—` |
| `ENGAGED_PAGE_VIEWS` | Betrokken paginaweergaven | Engaged page views | `#F3F4F6` | `—` |
| `ENGAGED_USERS` | Betrokken gebruikers | Engaged users | `#F3F4F6` | `—` |
| `EVENT_RESPONSES` | Evenementreacties | Event responses | `#F3F4F6` | `—` |
| `IMPRESSIONS` | Vertoningen | Impressions | `#F3F4F6` | `—` |
| `IN_APP_VALUE` | Waarde in app | In-app value | `#F3F4F6` | `—` |
| `LANDING_PAGE_VIEWS` | Landingspaginabezoeken | Landing page views | `#F3F4F6` | `—` |
| `LEAD_GENERATION` | Leadgeneratie | Lead generation | `#F3F4F6` | `—` |
| `LINK_CLICKS` | Linkklikken | Link clicks | `#F3F4F6` | `—` |
| `MEANINGFUL_CALL_ATTEMPT` | Betekenisvolle belpoging | Meaningful call attempt | `#F3F4F6` | `—` |
| `MESSAGING_APPOINTMENT_CONVERSION` | Conversie afspraak via berichten | Messaging appointment conversion | `#F3F4F6` | `—` |
| `MESSAGING_DEEP_CONVERSATION_AND_FOLLOW` | Diep gesprek en volgen via berichten | Messaging deep conversation and follow | `#F3F4F6` | `—` |
| `MESSAGING_PURCHASE_CONVERSION` | Aankoopconversie via berichten | Messaging purchase conversion | `#F3F4F6` | `—` |
| `NONE` | Geen | None | `#F3F4F6` | `—` |
| `OFFSITE_CONVERSIONS` | Externe conversies | Offsite conversions | `#F3F4F6` | `—` |
| `PAGE_LIKES` | Pagina-likes | Page likes | `#F3F4F6` | `—` |
| `POST_ENGAGEMENT` | Berichtbetrokkenheid | Post engagement | `#F3F4F6` | `—` |
| `PROFILE_AND_PAGE_ENGAGEMENT` | Profiel- en paginabetrokkenheid | Profile and page engagement | `#F3F4F6` | `—` |
| `PROFILE_VISIT` | Profielbezoek | Profile visit | `#F3F4F6` | `—` |
| `QUALITY_CALL` | Kwalitatief gesprek | Quality call | `#F3F4F6` | `—` |
| `QUALITY_LEAD` | Kwalitatieve lead | Quality lead | `#F3F4F6` | `—` |
| `REACH` | Bereik | Reach | `#F3F4F6` | `—` |
| `REMINDERS_SET` | Herinneringen ingesteld | Reminders set | `#F3F4F6` | `—` |
| `SUBSCRIBERS` | Abonnees | Subscribers | `#F3F4F6` | `—` |
| `THRUPLAY` | ThruPlay | ThruPlay | `#F3F4F6` | `—` |
| `VALUE` | Waarde | Value | `#F3F4F6` | `—` |
| `VISIT_INSTAGRAM_PROFILE` | Instagram-profiel bezoeken | Visit Instagram profile | `#F3F4F6` | `—` |

## Effective-status options

Reuse the single shared [`effective_status` property and complete 12-option set](meta-campaign.md#effective-status-options)
attached to Campaign, Ad Set, and Ad. Labels, colours, icons, and provider-level
applicability are maintained there; do not provision a separate subset for this object.

## Relations

- `conversion` ↔ `Candidate` (`candidate`), label **Conversie**. Reuse one shared relation definition across Campaign, Ad Set, and Ad. It links a candidate to each explicitly attributed Meta record; schema creation does not create record links or infer attribution from the parent hierarchy.

- `ad_set_campaign` → `Meta Campaign`.
- `ad_set_ads` → `Meta Ad`.

`campaign_id` and `campaign_name` are linked properties from the related Meta
Campaign. They must not be maintained as independent Ad Set values.
