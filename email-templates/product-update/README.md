# Caraer Product Update Email

Reusable, email-safe HTML template based on the current visual language of caraer.com.

## Files

- `template.html` — complete template with Release 1.9 example content.

## Before sending

1. Update the preheader, release label, headline, body copy, and feature content.
2. Replace both CTA destinations with the final campaign URLs.
3. Replace `{{ unsubscribe_url }}` with the unsubscribe token required by the sending platform.
4. Confirm that the Caraer app and release-page destinations are correct.
5. Send test messages to Outlook, Gmail, and Apple Mail before launching.

## Design system

- Primary pink: `#e74363`
- Ink: `#17181a`
- Warm background: `#f4f1ea`
- Headings: Georgia as the email-safe approximation of Caraer's New Kansas
- Body and UI: Arial/Helvetica as reliable email-safe sans-serif fonts
- Canvas: 660 px maximum width with a responsive mobile layout

## Compatibility choices

- Table-based layout for major email clients.
- Inline styles for reliable rendering.
- Responsive rules for screens below 680 px.
- VML fallbacks for primary Outlook buttons.
- Direct Sanity CDN image URLs instead of Caraer's Next.js image proxy.
- No JavaScript, forms, video, or CSS-dependent background images.
