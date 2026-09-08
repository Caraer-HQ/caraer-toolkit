# Core Capabilities

Caraer combines configurable recruitment data, websites, campaigns, AI, automation, communication, and reporting in one Recruitment Operating System.

## Time to Live

### Get your open positions online faster than ever

With features like **Smart Content** and **VacancyMaker™**, Caraer helps you create better vacancy content and get it online faster.

### Tools and features

- **VacancyMaker™ / AI vacancy creation** through configurable forms and Wizards.
- **Smart Content** for building and improving recruitment content around connected data.
- **Content Management System** for careers-site pages, components, settings, templates, and publishing.
- Website settings and digital identity management.
- Vacancy content, page content, images, CSS, previews, HTML snapshots, and design audits.
- Publishing and unpublishing for website content.

The live MCP tools supporting this pillar are listed in the verification snapshot below.

## Time to Launch

### Attract the right person for your vacancies

Start attracting candidates on autopilot, request custom campaigns, or integrate social-media lead-generation campaigns.

### Tools and features

- Job-board distribution through connected Apps.
- Social media recruitment campaigns.
- Social media lead-generation campaign integrations.
- Custom recruitment campaigns.
- Campaign previews and publication checks.
- Campaign, vacancy, candidate, and result data connected through records and relations.

The live MCP tools supporting this pillar are listed in the verification snapshot below.

## Time to Hire

### Candidate qualification and communication

Make your candidate journey a breeze.

Set up the system, candidate flow, and automations just as you need them. Everything is designed to reduce your time to hire.

- Use prebuilt AI candidate-qualification workflows.
- Edit and fine-tune workflows to match the organization’s process.
- Use WhatsApp workflows and AI Agents for candidate conversations and follow-up.
- Prioritize candidates and guide recruiters toward the next action.

### CV Parsing

CV Parsing returns structured candidate data from the full CV. The raw CV data is stored in a **Structure Property** as JSON, with relations to:

- Work Experience objects
- Education objects
- Skill objects

This makes the parsed CV available for candidate qualification, search, matching, workflows, and reporting.

## Time to Scale

### Recruitment database and talent pools

Scale up your recruitment efforts without anything getting in the way.

As soon as you have built a system that works, you need one that can grow. Caraer helps you scale towards your next recruitment target.

- Create custom objects for the organization’s recruitment model.
- Define properties, relations, and access around the organization’s data.
- Build talent pools through the database and relations.
- Connect candidates, vacancies, companies, campaigns, communication, and outcomes.

### Automation and integrations

- Build workflows around recruitment events and processes.
- Use prebuilt workflows and AI Agents as starting points.
- Adapt automations instead of treating them as fixed black boxes.
- Connect external services through Apps and integrations.

### Reporting and dashboards

- Add the Analytics trait to any object so its records can contribute to reporting.
- Use a central dashboard to combine recruitment data across objects, teams, brands, and processes.
- Monitor campaign performance, candidate progress, workflow outcomes, and other recruitment measures.

## Configured capabilities by product pillar

Some Caraer capabilities are delivered through configured forms, Wizards, Apps, workflows, and AI Agents. They should not be treated as unavailable just because the MCP exposes no single tool with the same business name.

### Time to Live

| Business capability | How it is delivered | MCP foundation |
| --- | --- | --- |
| AI vacancy creation | Forms and Wizards with configurable AI-assisted vacancy creation | Forms, webpages, objects, properties, and records |

### Time to Launch

| Business capability | How it is delivered | MCP foundation |
| --- | --- | --- |
| Campaign distribution | Apps for job boards and social media campaigns | Webpages, previews, records, and configured Apps |

### Time to Hire

| Business capability | How it is delivered | MCP foundation |
| --- | --- | --- |
| AI candidate qualification | Prebuilt workflows that customers can edit and fine-tune | Records, queries, relations, and configured automation |
| WhatsApp conversations | Prebuilt workflows and AI Agents in Automations | Records, relations, and configured communication integrations |

### Time to Scale

| Business capability | How it is delivered | MCP foundation |
| --- | --- | --- |
| Talent pools | Configurable database setup and relations | Objects, properties, records, and relations |
| Custom objects | Organization-specific recruitment database management | Objects, properties, relations, and traits |
| Analytics and central dashboards | Analytics trait on any object plus a central dashboard | Traits, previews, queries, and records |

## Contact

For a walkthrough of the capabilities relevant to your organization, contact [hello@caraer.com](mailto:hello@caraer.com) or [book a demo at caraer.com/demo](https://caraer.com/demo).

<!-- capability-audit:start -->
## Verification snapshot

This section is maintained by the monthly capability review. It records technical source checks and maps the live MCP tools to Caraer’s four product pillars; it does not replace the product descriptions above.

- Last checked: 2026-09-01, 3:15 a.m. Europe/Amsterdam
- Website: 200 OK; title: We help companies become candidate magnets | Caraer; content hash: `00c714ed43f3b022`; detected signals: vacancies, candidates, campaigns, AI, automation, dashboards, VacancyMaker, Smart Content, CMS, CV Parsing
- Caraer MCP: 200 OK; 73 tools; server: caraer-mcp 1.0.0; resources: 0; templates: 0; ungrouped descriptions: 73; detected capability signals in tool names: CMS

## MCP tools by product pillar

Tools are assigned to their primary product pillar for documentation and support. A tool may support more than one workflow in practice. Job-board and social-media campaign Apps, customer workflows, and AI Agents are configured capabilities and are not necessarily represented as dedicated MCP tool names.

### Time to Live

- `company_digital_identity_get`
- `company_digital_identity_update`
- `company_website_settings_get`
- `company_website_settings_update`
- `form_create`
- `form_get`
- `form_index`
- `form_update`
- `webpage_content_children_replace`
- `webpage_content_css_set`
- `webpage_content_node_delete`
- `webpage_content_node_upsert`
- `webpage_content_schema_help`
- `webpage_content_summary`
- `webpage_design_audit`
- `webpage_get`
- `webpage_html_snapshot`
- `webpage_image_upload`
- `webpage_publish`
- `webpage_template_get`
- `webpage_template_upsert`
- `webpage_unpublish`
- `webpage_upsert`

### Time to Launch

- `preview_create_or_update`
- `preview_get`
- `preview_grid_examples`
- `preview_list`
- `preview_list_all`

### Time to Hire

- `record_bulk_edit`
- `record_create`
- `record_create_or_update`
- `record_create_or_update_relation`
- `record_create_relation`
- `record_delete`
- `record_delete_relation`
- `record_extend`
- `record_get`
- `record_get_by_unique`
- `record_list`
- `record_query`
- `record_restore`
- `record_search`
- `record_update`
- `relation_create_or_update`
- `relation_get`
- `relation_list`
- `relation_list_for_object`

### Time to Scale

- `access_scopes_get`
- `object_create`
- `object_get`
- `object_list`
- `object_sync_extended_objects`
- `object_update`
- `property_create`
- `property_formats_list`
- `property_get`
- `property_list`
- `property_types_list`
- `property_update`
- `property_value_shapes_list`
- `record_filter_examples`
- `record_filter_operators_list`
- `record_pagination_schema`
- `record_query_schema`
- `relation_properties_attach`
- `relation_properties_detach`
- `relation_properties_list`
- `schema_help`
- `trait_create_or_update`
- `trait_delete`
- `trait_get`
- `trait_list`
- `trait_types_list`
<!-- capability-audit:end -->
