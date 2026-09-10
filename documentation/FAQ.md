# Frequently Asked Questions

Short answers to common questions about Caraer. Follow the links for more detailed guidance.

## General

### What is Caraer?

Caraer is a configurable Recruitment Operating System. It brings careers sites, vacancies, recruitment campaigns, candidates, communication, automation, and recruitment data together in one platform.

See [About Caraer](About%20Caraer/about_caraer.md) and [Core Capabilities](About%20Caraer/core_capabilities.md).

### Is Caraer only an applicant tracking system (ATS)?

No. Caraer supports the wider recruitment journey: creating and publishing vacancies, launching campaigns, managing and qualifying candidates, communicating with candidates, automating work, and reporting on recruitment data.

See [About Caraer](About%20Caraer/about_caraer.md).

### Who is Caraer for?

Caraer can be configured for corporate recruitment teams, recruitment agencies, enterprise organisations, SMEs, and independent recruiters.

See [Who Caraer Is For](About%20Caraer/target_audience.md).

## Data and records

### What is the difference between an Object, a Record, and a Property?

- An **Object** describes a kind of information, such as Company, Contact, or Task.
- A **Record** is one individual item of that Object.
- A **Property** stores a piece of information on a Record, such as a name, status, or date.

See [Objects Schema](Data/Objects%20Schema.md).

### When should I use a Relation instead of a Property?

Use a Property for information about one Record. Use a Relation when the information should connect to another independent Record with its own data or lifecycle.

See [Relations](Data/Relations.md).

### Do Views or Filters change my Records?

No. Views and Filters change which Records you see and how they are organised. They do not duplicate, delete, or otherwise change the underlying Records. Editing a Record from within a View does change that Record.

See [Views and Filters](Data/Views%20and%20Filters.md).

## Users and access

### Why can’t I see or edit something?

Your access may depend on your User, Team, Suite, Scope, and Authorisations. You may be allowed to view information without being allowed to edit or manage it. Ask your Caraer administrator or representative to review your access if an option is missing.

See [Users & Access](Users%20%26%20Access/README.md) and [Authorisations](Users%20%26%20Access/Authorisations.md).

### What should happen when someone joins, changes role, or leaves?

Review their access and give them only what they need for their work. Remove or adjust access promptly when responsibilities change or someone leaves the organisation.

See [Users](Users%20%26%20Access/Users.md).

## Automations

### How do I copy a Scenario in Automations?

1. Open the **Scenarios** page.
2. Open the menu (**⋯**) for the Scenario you want to copy.
3. Select **Copy**.
4. Create or open the Scenario where you want the copy.
5. Right-click an empty area of the canvas and select **Paste**.
6. Rename the copied Scenario, review its settings, and test it before activation.

Routes and Node settings are retained. If the Scenario contains a **Trigger on Webhook**, change the duplicated webhook address so it is unique. Authorisations are retained when copying within the same account, but must be configured again when copying between accounts.

See [Scenarios](Automations/01%20Scenarios/01%20Scenarios.md#copy-a-scenario).

### What is a Scenario?

In Caraer Automations, a Scenario is a chain of connected Nodes. A trigger starts the Scenario, and each Node performs a step and passes its result to the next Node.

See [Scenarios](Automations/01%20Scenarios/01%20Scenarios.md) and [Nodes](Automations/02%20Nodes.md).

### How should I build and test an Automation?

Start with the result you want, choose the trigger and Nodes, connect the steps, and test each Node in order. Inspect the output and confirm the development or production behaviour before activating the Scenario for real events.

See [Scenarios](Automations/01%20Scenarios/01%20Scenarios.md) and [Data Flow](Automations/09%20Data%20Flow.md).

## CMS

### Where do I organise website pages and navigation?

Use the CMS Structure page at `/structure`. It can organise pages, sections, navigation, URLs, and relationships between content items.

See [CMS Structure](CMS/Structure.md).

## Support

### What should I include when asking for help?

Include what you were trying to do, what happened, what you expected, and the affected page or Record. Add the exact error message and a screenshot when available. Do not include passwords, access tokens, or other secrets.

For questions about your account, contract, plan, usage, or access, contact your Caraer representative so the relevant account information can be checked securely.

## Keeping this FAQ useful

This FAQ should grow from real customer questions. Add or update an answer only after it has been verified against the maintained Caraer documentation or the relevant product owner. Keep detailed instructions in the appropriate product section and use this page as a concise entry point.
