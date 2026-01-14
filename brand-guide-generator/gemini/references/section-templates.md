# Section Templates

Detailed templates for each brand guide section. Adapt depth based on company stage.

---

## 1. Brand Overview

```markdown
# [Company Name] Brand Guidelines

## Brand Overview

### Our Mission
[One sentence: what the company does and why it matters]

### Our Vision
[One sentence: the future state the company is working toward]

### Brand Promise
*[Tagline or brand promise - italicized, memorable]*

### Brand Personality

| Trait | Description | How It Shows Up |
|-------|-------------|-----------------|
| [Trait 1] | [Brief definition] | [Concrete example] |
| [Trait 2] | [Brief definition] | [Concrete example] |
| [Trait 3] | [Brief definition] | [Concrete example] |
| [Trait 4] | [Brief definition] | [Concrete example] |

### What We Are / What We're Not

| We Are | We're Not |
|--------|-----------|
| [Positive trait] | [Opposite to avoid] |
| [Positive trait] | [Opposite to avoid] |
| [Positive trait] | [Opposite to avoid] |
```

---

## 2. Logo

```markdown
## Logo

### Primary Logo
[Description of logo - wordmark, logomark, or combination]

### Logo Versions
| Version | Use Case | File |
|---------|----------|------|
| Primary (Color) | Light backgrounds, primary use | `logo-primary.svg` |
| Reversed (White) | Dark backgrounds | `logo-white.svg` |
| Mono (Black) | Single-color print | `logo-black.svg` |
| Icon Only | Favicons, app icons, small spaces | `logo-icon.svg` |

### Clear Space
Maintain clear space equal to [X] around all sides of the logo.
[Include visual diagram if possible]

### Minimum Sizes
| Context | Minimum Width |
|---------|---------------|
| Digital | [X]px |
| Print | [X]mm |

### Logo Don'ts
- ❌ Don't stretch or distort
- ❌ Don't rotate
- ❌ Don't change colors outside brand palette
- ❌ Don't add shadows, gradients, or effects
- ❌ Don't place on busy backgrounds without sufficient contrast
- ❌ Don't outline or contain in shapes
- ❌ Don't rearrange logo elements
```

---

## 3. Color Palette

```markdown
## Color Palette

### Primary Colors

| Color | Name | HEX | RGB | Use |
|-------|------|-----|-----|-----|
| [swatch] | [Name] | #XXXXXX | X, X, X | [Primary use case] |
| [swatch] | [Name] | #XXXXXX | X, X, X | [Primary use case] |
| [swatch] | [Name] | #XXXXXX | X, X, X | [Primary use case] |

### Secondary Colors

| Color | Name | HEX | RGB | Use |
|-------|------|-----|-----|-----|
| [swatch] | [Name] | #XXXXXX | X, X, X | [Use case] |
| [swatch] | [Name] | #XXXXXX | X, X, X | [Use case] |

### Semantic / UI Colors

| Color | Name | HEX | Use |
|-------|------|-----|-----|
| 🟢 | Success | #XXXXXX | Success states, confirmations |
| 🟡 | Warning | #XXXXXX | Warnings, caution states |
| 🔴 | Error | #XXXXXX | Errors, destructive actions |
| 🔵 | Info | #XXXXXX | Informational messages |

### Color Usage Rules
1. Primary color should appear in every piece of collateral
2. Maintain WCAG AA contrast ratios (4.5:1 for normal text)
3. Use semantic colors only for their intended purpose
4. White space is essential—don't overcrowd with color

### CSS Variables
```css
:root {
  /* Primary */
  --color-primary: #XXXXXX;
  --color-primary-dark: #XXXXXX;
  --color-primary-light: #XXXXXX;
  
  /* Neutrals */
  --color-text: #XXXXXX;
  --color-text-secondary: #XXXXXX;
  --color-background: #XXXXXX;
  --color-surface: #XXXXXX;
  --color-border: #XXXXXX;
  
  /* Semantic */
  --color-success: #XXXXXX;
  --color-warning: #XXXXXX;
  --color-error: #XXXXXX;
}
```
```

---

## 4. Typography

```markdown
## Typography

### Primary Typeface: [Font Name]

[Brief description of why this font was chosen and its characteristics]

**Font Stack:**
```css
font-family: '[Font Name]', [fallback1], [fallback2], sans-serif;
```

**Source:** [Google Fonts / Adobe Fonts / Custom]

### Type Scale

| Use | Size | Weight | Line Height | Letter Spacing |
|-----|------|--------|-------------|----------------|
| Display / Hero | 48px (3rem) | 700 | 1.1 | -0.02em |
| H1 | 36px (2.25rem) | 700 | 1.2 | -0.01em |
| H2 | 30px (1.875rem) | 600 | 1.2 | 0 |
| H3 | 24px (1.5rem) | 600 | 1.3 | 0 |
| H4 | 20px (1.25rem) | 600 | 1.4 | 0 |
| Body Large | 18px (1.125rem) | 400 | 1.6 | 0 |
| Body | 16px (1rem) | 400 | 1.6 | 0 |
| Body Small | 14px (0.875rem) | 400 | 1.5 | 0 |
| Caption | 12px (0.75rem) | 500 | 1.4 | 0.01em |

### Typography Rules
1. Headlines: Use [weight] weight, tight line-height
2. Body text: Regular weight (400), generous line-height (1.5-1.6)
3. Maximum line length: 65-75 characters for readability
4. Never use weights below 400 for body text
5. Limit to 2-3 type sizes per design

### Font Loading (Web)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=[FontName]:wght@400;500;600;700&display=swap" rel="stylesheet">
```
```

---

## 5. Voice & Tone

```markdown
## Voice & Tone

### Brand Voice Principles

**1. [Principle Name]**
[Description of principle]

✅ Do: "[Good example]"
❌ Don't: "[Bad example]"

**2. [Principle Name]**
[Description of principle]

✅ Do: "[Good example]"
❌ Don't: "[Bad example]"

**3. [Principle Name]**
[Description of principle]

✅ Do: "[Good example]"
❌ Don't: "[Bad example]"

**4. [Principle Name]**
[Description of principle]

✅ Do: "[Good example]"
❌ Don't: "[Bad example]"

### Tone by Context

| Context | Tone | Example |
|---------|------|---------|
| Marketing | [Tone descriptors] | "[Example copy]" |
| Product UI | [Tone descriptors] | "[Example copy]" |
| Sales | [Tone descriptors] | "[Example copy]" |
| Support | [Tone descriptors] | "[Example copy]" |
| Technical Docs | [Tone descriptors] | "[Example copy]" |

### Words We Use / Words We Avoid

| Use | Avoid |
|-----|-------|
| [Preferred term] | [Term to avoid] |
| [Preferred term] | [Term to avoid] |
| [Preferred term] | [Term to avoid] |

### Writing Checklist
- [ ] Is it clear on first read?
- [ ] Does it sound like our brand?
- [ ] Is it appropriate for the audience?
- [ ] Does it drive action?
- [ ] Is it free of jargon (unless intentional)?
```

---

## 6. Visual Identity

```markdown
## Visual Identity

### Design Principles
1. **[Principle]**: [Description]
2. **[Principle]**: [Description]
3. **[Principle]**: [Description]
4. **[Principle]**: [Description]

### Imagery Style

**Do use:**
- [Description of appropriate imagery]
- [Description of appropriate imagery]
- [Description of appropriate imagery]

**Don't use:**
- [Description of imagery to avoid]
- [Description of imagery to avoid]
- [Description of imagery to avoid]

### Iconography
- Style: [Line / Solid / Duotone]
- Stroke weight: [X]px
- Default size: [X]px
- Colors: [Default color] for inactive, [Primary color] for active
- Recommended set: [Icon library name]

### Layout & Spacing
- **Base unit:** 8px
- **Border radius:** [X]px (cards), [X]px (buttons), [X]px (inputs)
- **Grid:** 12-column
- **Max content width:** [X]px

### Component Patterns

**Buttons:**
- Primary: [Background], [Text], [Border radius]
- Secondary: [Background], [Border], [Text]
- Sizing: [Padding values]

**Cards:**
- Background: [Color]
- Border radius: [X]px
- Shadow: [Shadow values]
- Padding: [X]px

**Form Inputs:**
- Border: [Border style]
- Border radius: [X]px
- Focus state: [Description]
```

---

## 7. Applications

```markdown
## Applications

### Email Signature
```
[Name]
[Title] | [Company]

[email] | [website]
```

### Business Card Layout
- Front: Logo centered, tagline below
- Back: Name, title, contact details
- Size: 3.5" × 2" (standard) or 85mm × 55mm

### Presentation Template
- Title slide: Logo [position], title centered
- Content slides: Logo [position], consistent header style
- Charts/data: Use brand colors only

### Social Media

**Profile Images:**
- Use logo icon version
- Ensure legibility at small sizes

**Post Templates:**
- Maintain consistent visual style
- Use brand colors for overlays/graphics
- Typography: [Font] for any text overlays

### Document Headers
- Logo: [Position], [Size]
- Page numbers: [Position]
- Margins: [Values]
```

---

## 8. Quick Reference Card

```markdown
## Quick Reference

| Element | Specification |
|---------|---------------|
| Primary Color | #XXXXXX |
| Secondary Color | #XXXXXX |
| Text Color | #XXXXXX |
| Background | #XXXXXX |
| Font | [Font Name] |
| Body Size | 16px |
| Border Radius | [X]px |
| Spacing Unit | 8px |

### Logo Files
- Primary: `logo-primary.svg`
- White: `logo-white.svg`
- Icon: `logo-icon.svg`

### Key Contacts
- Brand questions: [email]
- Asset requests: [email/location]
```
