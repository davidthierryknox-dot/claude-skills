# Color Palette Reference

Guidance for extracting, validating, and building brand color palettes.

---

## Color Extraction from Websites

When analyzing an existing website, look for:

1. **Primary brand color**: Usually in logo, buttons, links, headers
2. **Secondary colors**: Accent elements, highlights, secondary CTAs
3. **Neutral palette**: Text colors, backgrounds, borders
4. **Semantic colors**: Success/error/warning states (often green/red/yellow)

### Common Extraction Points
- Logo (dominant color)
- Primary CTA buttons
- Link colors
- Header/navigation background
- Footer background
- Highlight/accent elements

### Validation Checks
After extracting colors, verify:
- [ ] Primary color is distinct and memorable
- [ ] Text colors meet WCAG AA contrast (4.5:1 minimum)
- [ ] Colors work together harmoniously
- [ ] Palette isn't too large (aim for 8-12 total colors max)

---

## Building a Palette from Scratch

### Minimum Viable Palette (Startup)

| Role | Count | Description |
|------|-------|-------------|
| Primary | 1 | Hero brand color |
| Primary variants | 2 | Lighter + darker for hover/backgrounds |
| Neutral text | 2 | Primary text + secondary text |
| Neutral background | 2 | White + light gray |
| Semantic | 3 | Success, warning, error |

**Total: ~10 colors**

### Full Palette (Growth/Enterprise)

| Role | Count | Description |
|------|-------|-------------|
| Primary | 1 | Hero brand color |
| Primary scale | 5-9 | Full tint/shade scale |
| Secondary | 1-2 | Complementary accent colors |
| Secondary scale | 3-5 each | Tint/shade scales |
| Neutral scale | 9-11 | Full gray scale from white to near-black |
| Semantic | 3-4 | Success, warning, error, info |
| Semantic variants | 2-3 each | Light/dark variants |

**Total: 30-50 colors**

---

## Industry Color Conventions

### Finance / Fintech
- Blues (trust, stability): #1E3A8A, #2563EB, #3B82F6
- Greens (money, growth): #059669, #10B981
- Avoid: Bright reds (debt associations), overly playful colors

### Healthcare / Healthtech
- Blues (calm, clinical): #0EA5E9, #06B6D4
- Greens (health, nature): #22C55E, #84CC16
- Teals (medical, clean): #14B8A6, #2DD4BF
- Avoid: Harsh reds, aggressive colors

### B2B SaaS / Enterprise
- Blues (professional, tech): #2563EB, #4F46E5
- Purples (innovation): #7C3AED, #8B5CF6
- Teals (modern): #0D9488, #14B8A6
- Clean neutrals essential

### Consumer / E-commerce
- More freedom—personality-driven
- Warm colors (engagement): Oranges, corals
- Consider: Accessibility for diverse audiences

### Legal / Professional Services
- Conservative palettes
- Deep blues: #1E3A5F, #1E40AF
- Burgundy/maroon: #7F1D1D, #991B1B
- Minimal accent colors

---

## Recommended Color Palettes

### Modern Blue (B2B SaaS Default)
```
Primary:      #2563EB (Blue)
Primary Dark: #1D4ED8
Primary Light:#DBEAFE
Text:         #1E293B
Text Muted:   #64748B
Background:   #FFFFFF
Surface:      #F8FAFC
Border:       #E2E8F0
Success:      #10B981
Warning:      #F59E0B
Error:        #EF4444
```

### Trustworthy Teal (Fintech/Health)
```
Primary:      #0D9488 (Teal)
Primary Dark: #0F766E
Primary Light:#CCFBF1
Text:         #134E4A
Text Muted:   #5EEAD4
Background:   #FFFFFF
Surface:      #F0FDFA
Border:       #99F6E4
Success:      #22C55E
Warning:      #EAB308
Error:        #DC2626
```

### Bold Purple (Innovation/Creative)
```
Primary:      #7C3AED (Purple)
Primary Dark: #6D28D9
Primary Light:#EDE9FE
Text:         #1E1B4B
Text Muted:   #6B7280
Background:   #FFFFFF
Surface:      #FAF5FF
Border:       #E9D5FF
Success:      #22C55E
Warning:      #F59E0B
Error:        #EF4444
```

### Warm Coral (Consumer/Friendly)
```
Primary:      #F97316 (Orange)
Primary Dark: #EA580C
Primary Light:#FFEDD5
Text:         #1C1917
Text Muted:   #78716C
Background:   #FFFFFF
Surface:      #FFFBEB
Border:       #FED7AA
Success:      #22C55E
Warning:      #EAB308
Error:        #DC2626
```

### Professional Navy (Enterprise/Legal)
```
Primary:      #1E3A8A (Navy)
Primary Dark: #1E40AF
Primary Light:#DBEAFE
Text:         #111827
Text Muted:   #6B7280
Background:   #FFFFFF
Surface:      #F9FAFB
Border:       #E5E7EB
Success:      #059669
Warning:      #D97706
Error:        #DC2626
```

---

## Color Format Reference

Always provide colors in multiple formats:

### HEX
`#2563EB`

### RGB
`37, 99, 235` or `rgb(37, 99, 235)`

### HSL
`217, 91%, 53%` or `hsl(217, 91%, 53%)`

### CSS Custom Property
```css
--color-primary: #2563EB;
```

### Tailwind Config
```js
primary: {
  DEFAULT: '#2563EB',
  50: '#EFF6FF',
  100: '#DBEAFE',
  // ... full scale
  900: '#1E3A8A',
}
```

---

## Accessibility Requirements

### WCAG Contrast Ratios

| Use Case | Minimum Ratio | Requirement Level |
|----------|---------------|-------------------|
| Normal text | 4.5:1 | AA |
| Large text (18px+ or 14px bold) | 3:1 | AA |
| UI components & graphics | 3:1 | AA |
| Normal text | 7:1 | AAA |
| Large text | 4.5:1 | AAA |

### Quick Contrast Checks

For #2563EB (Manzas Blue):
- ✅ White text on blue: 4.56:1 (passes AA)
- ✅ Blue text on white: 4.56:1 (passes AA)
- ❌ Blue text on light blue (#DBEAFE): 3.2:1 (fails for small text)

### Tools for Validation
- WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/
- Coolors Contrast Checker: https://coolors.co/contrast-checker
- Chrome DevTools color picker (shows contrast)

---

## Generating Color Scales

For a primary color, generate a full scale:

### Tint/Shade Scale Pattern
```
50:  Very light (backgrounds)
100: Light (hover backgrounds)
200: Light accent
300: Medium light
400: Medium
500: Base color (PRIMARY)
600: Medium dark (hover)
700: Dark
800: Very dark
900: Near black (text on light)
```

### Quick Scale Generation
Use tools:
- Tailwind CSS color generator: https://uicolors.app/create
- Palx: https://palx.jxnblk.com/
- Leonardo: https://leonardocolor.io/