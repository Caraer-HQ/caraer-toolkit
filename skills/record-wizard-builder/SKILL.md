---
name: "record-wizard-builder"
description: "Design and create reusable multistep record-creation wizards for Caraer Forms."
---

# Record wizard builder

Use for intuitive Caraer Forms that create one record of any object type, such as an Event, Vacancy, or future record type.

## Workflow

1. Inspect the target portal, object schema, properties, options, required rules, relations, formats, and existing forms.
2. Classify fields as user-entered, hidden/defaulted, derived website fields, internal workflow data, or relation data.
3. Check central wizard templates and design from structured facts to prose/assets.
4. Build a field contract for every user-facing field before creating the form.
5. Check renderer capabilities before using conditional logic, dynamic review, nested forms, date/time input, or structured/JSON fields.
6. Start with a navigation `section`, followed immediately by a visible `Intro` step; prefer two or more sections with related steps.
7. Begin data entry with the record title, then facts, then prose/assets.
8. Present the plan for approval before changing a live form.
9. Use `/forms/<form-name>`; localized forms may use a localized public label while the internal name remains stable.
10. After every live write, retrieve and verify order, styling, layout, labels, defaults, prompts, one submit button, review/submit behavior, thank-you message, and URL.

## Universal field contracts

Define a compact contract before mapping fields to Forms MCP:

```yaml
field: registration_deadline
purpose: deadline for registration
input: date
required: false
visibility:
  when:
    property: registration_required
    equals: true
fallback: separate_step
public: true
ai_context: false
```

A field contract may include:

- source property and storage type;
- user-facing purpose;
- input/format;
- requiredness and safe default;
- public versus internal visibility;
- conditional visibility rule;
- fallback when the renderer lacks that capability;
- AI context eligibility;
- validation and error guidance.

Keep contracts generic. Do not encode customer names, branding, or one object type into the reusable skill.

## Capability-aware conditional logic

Represent conditional behaviour abstractly, then compile it only when the Forms renderer supports it.

1. Inspect and verify the capability before using it.
2. If supported, translate the rule to the actual MCP schema.
3. If unsupported, use the contract's fallback: a separate explanatory step, an optional field, or a post-submit workflow.
4. Never send undocumented conditional settings or claim that static hidden/default settings are conditional.
5. Record unsupported capabilities as a limitation when they materially affect the user experience.

The same approach applies to dynamic review summaries, date/time controls, nested forms, repeatable groups, and structured inputs.

## Form MCP constraints

- `form_create` requires name, object, and grids; use `wizard: true` for multiple grids.
- Exactly one `submitButton` is allowed across a form.
- A cell can contain property, text, nested form, or submit button.
- Field labels are not rendered automatically. Cell settings include label, placeholder, isRequired, hidden, defaultValue, helpText, styling, stretch, align, rangeMin, and rangeMax.
- Use real property options. Inspect object, properties, formats, and existing forms first.
- Validate date capability before saying “date and time”; document a bug if time-of-day is unsupported.
- Do not use a structure/JSON property unless renderer editing is verified; prefer multiline text.
- Check existing active and soft-deleted forms before choosing a name. Do not invent a suffix or assume a deleted name is reusable when the API reports a duplicate.
- If form deletion or restoration is not exposed, report the exact limitation and preserve the local source snapshot.

## Intro, headings, labels, and grids

- A section may only provide navigation and may not render as a visible page. Always use a separate first `step` named `Intro` when intro content must be shown.
- Put intro content in one text cell: a Markdown H1 and a welcoming/appreciation paragraph. Do not split it into multiple text cells merely for spacing.
- Keep intro copy generic and audience-appropriate; never hard-code a customer name in this reusable skill.
- Use a static explanatory text cell above each user-facing input.
- Treat explanatory text as Markdown. Use `# Heading` for the Intro H1; use `### Heading` (or `####` for a smaller hierarchy) for subsequent step questions.
- Put a question heading and its short explanatory subtitle in the same text cell, separated by a blank line.
- For a single-select, the Markdown heading is the visible question; omit the property label because one grid option is self-explanatory.
- For a multi-select, use a Markdown heading for the question and the standard property label `Meerdere opties mogelijk` or its localized equivalent.
- For text fields with explanatory text and an example placeholder, omit the property label.
- A single-select or multi-select gets its own step by default, with cell `settings.styling: "grid"`.
- Sections group navigation; grids are ordered arrays of rows and cells. Multiple cells in one row are deliberately side-by-side.
- Prefer short descriptive step titles, ideally one word; use longer titles only when needed for clarity.
- Use a default value rather than a placeholder when the value is a common editable starting point. Never use a default to hide uncertainty.
- Keep review/submit as the final step and verify mobile rendering.

## Selection and boolean requirements

- Never require a user-facing single-select or multi-select by default. Keep property rules and form-cell `isRequired` false unless a genuinely mandatory selection is explicitly confirmed.
- Never require a checkbox by default. Required checkboxes are limited to explicit acknowledgement/consent; ordinary yes/no facts remain optional with safe defaults.
- Hidden defaulted system fields are not required.
- Audit property and form levels; form false does not override a property required rule. If an existing schema violates this rule, remove the unintended property rule and set the form cell false, then retrieve and verify.

## Progressive AI assistance

Collect facts first, then assist with prose. Every AI-assisted field should have an explicit contract:

```yaml
field: invitation_text
goal: inviting copy for the intended audience
context:
  - title
  - type
  - audience
  - location
output:
  language: nl
  tone: warm and inviting
  length: 60-100 words
rules:
  - use only supplied facts
  - invent no dates, prices, promises, or logistics
  - return an editable draft
privacy:
  exclude:
    - internal notes
    - private contact details
```

Rules:

1. Collect names/types, dates/times, location, audience, price, registration, roles, departments, and requirements before prose.
2. Whitelist completed structured fields as AI context; do not forward the entire record by default.
3. Specify target field, audience, language, tone, length, format, and factual boundaries.
4. Distinguish `suggest`, `rewrite`, and `shorten` behaviours where the renderer supports them.
5. Use step-level `AIPrompt` unless field-level support is validated; do not rely on undocumented interpolation.
6. Keep generated text editable and separate from source facts; never overwrite structured fields.
7. Treat generated text as a draft requiring user review.
8. Provide static help/placeholder text when AI assistance is unavailable.
9. Never include internal assignments, private contact data, or unrelated sensitive fields in AI context.

## Wizard quality score

Run a quality check before and after creation. Use:

- ✅ pass;
- ⚠️ attention required;
- ❌ blocking issue.

Block on:

- missing visible Intro step when intro content is required;
- no clear title field near the start;
- missing or invalid object property reference;
- more than one submit button;
- required select or checkbox without explicit justification;
- unverified structure/JSON or unsupported dynamic behaviour;
- missing persisted-state verification after a live write.

Warn on:

- long or vague step titles;
- multiple unrelated decisions in one step;
- multiline text without explanatory context or example;
- unnecessary duplicate labels;
- side-by-side layout that is questionable on mobile;
- AI prompt without whitelisted context, language, tone, length, or anti-invention rule;
- unsafe or unexplained defaults;
- public fields mixed with internal planning data;
- no clear post-submit expectation.

A passing score does not replace a human review of language, accessibility, and mobile rendering.

## Review, submission, and safety

- Include a final review step with concise instructions and one submit button.
- Forms MCP has no verified dynamic review/summary control; users review by navigating back.
- Configure `thankYouMessage` to confirm record creation, initial status, and next action.
- Keep publication and other external side effects separate from submission unless explicitly approved.
- Model people, teams, and organisations as relations, using post-submit workflow or approved inner forms for dynamic relation selection.
- Ask before changing live schema, relations, permissions, or publishing; preserve existing forms and verify every live write.
- Keep customer-specific details out of this reusable skill.
