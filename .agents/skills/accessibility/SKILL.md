---
name: accessibility
description: Web accessibility auditing and remediation for HTML content. Use when creating, reviewing, or fixing HTML/CSS/JavaScript to ensure WCAG compliance, screen reader compatibility, keyboard navigation, color contrast, semantic markup, and inclusive design. Triggers on requests involving accessibility, a11y, WCAG, ARIA, screen readers, or making content usable for people with disabilities.
---

# Web Accessibility Skill

## Core Principles (WCAG POUR)
- **Perceivable**: Content available to all senses (alt text, captions, contrast)
- **Operable**: All functionality via keyboard, no time traps, no seizure triggers
- **Understandable**: Readable, predictable, input assistance provided
- **Robust**: Works with assistive technologies, valid markup

## Quick Audit Checklist

### Images & Media
- All `<img>` have meaningful `alt` (or `alt=""` for decorative)
- Complex images have extended descriptions
- Videos have captions and transcripts
- Audio has transcripts

### Semantic HTML
- Use `<header>`, `<nav>`, `<main>`, `<footer>`, `<article>`, `<section>`
- Headings in logical order (`h1` → `h2` → `h3`), no skipped levels
- Lists use `<ul>`, `<ol>`, `<dl>` appropriately
- Tables have `<th>`, `scope`, and `<caption>`

### Keyboard & Focus
- All interactive elements reachable via Tab
- Visible focus indicator (never `outline: none` without replacement)
- Logical tab order (avoid positive `tabindex`)
- No keyboard traps
- Skip links for main content: `<a href="#main" class="skip-link">Skip to content</a>`

### Forms
- Every input has associated `<label>` (use `for`/`id` or wrap)
- Required fields marked with `aria-required="true"` and visual indicator
- Error messages linked with `aria-describedby`
- Group related fields with `<fieldset>` and `<legend>`

### Color & Contrast
- Text contrast ratio: 4.5:1 minimum (3:1 for large text 18px+ bold or 24px+)
- Never convey info by color alone (add icons, text, patterns)
- Test with grayscale filter

### ARIA (use sparingly)
- Prefer native HTML elements over ARIA
- If ARIA needed: `role`, `aria-label`, `aria-labelledby`, `aria-describedby`
- Live regions for dynamic content: `aria-live="polite"` or `aria-live="assertive"`
- State attributes: `aria-expanded`, `aria-selected`, `aria-checked`, `aria-hidden`

### Interactive Components
```html path=null start=null
<!-- Button (not div/span) -->
<button type="button">Click me</button>

<!-- Link (has href) -->
<a href="/page">Go somewhere</a>

<!-- Custom widget needs role + keyboard -->
<div role="button" tabindex="0" 
     onkeydown="if(event.key==='Enter'||event.key===' ')this.click()">
  Custom button
</div>
```

### Common Fixes

**Missing document language:**
```html path=null start=null
<html lang="en">
```

**Missing page title:**
```html path=null start=null
<title>Descriptive Page Title</title>
```

**Inaccessible icon button:**
```html path=null start=null
<!-- Bad -->
<button>×</button>

<!-- Good -->
<button aria-label="Close dialog">×</button>
```

**Touch targets (mobile):**
- Minimum 44×44px for touch targets
- Adequate spacing between targets

## Testing Approach
1. Keyboard-only navigation (Tab, Shift+Tab, Enter, Space, Arrows)
2. Screen reader testing (VoiceOver, NVDA)
3. Browser extensions: axe DevTools, WAVE
4. Contrast checker tools
5. Zoom to 200% - content should reflow

## When Reviewing Code
- Flag missing alt text, labels, landmarks
- Check color contrast on custom colors
- Verify keyboard handlers on custom components
- Ensure focus management in modals/dialogs
- Validate ARIA usage (roles match behavior)

