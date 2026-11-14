# Caraer Lead & Demo Report Email

Reusable responsive HTML layout for an internal daily summary of lead activity, qualification, upcoming demos, and follow-ups.

## Files

- `template.html` — email-safe report layout with placeholders for report data.

## Before rendering

1. Populate every `{{placeholder}}` from verified current data; HTML-escape all record-derived text.
2. Preserve unknown or inaccessible values as unknown rather than displaying them as zero or “None”.
3. Keep qualified and new lead rows distinct and deduplicate records that appear in both sections.
4. Include the reporting period and generation time, and explain any data-coverage limitations.
5. Render alerts only from verified evidence and ensure all placeholders are resolved before delivery.
6. Send only through an approved internal workflow and verify the final message after delivery.

This toolkit template contains no real lead records, recipient list, schedule, credentials, or collection configuration. It is a layout, not a ready-to-send report.
