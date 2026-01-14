# Typography Reference

Font recommendations, pairings, and implementation guidance.

---

## Recommended Fonts by Use Case

### Modern Sans-Serif (Default Recommendation)

| Font | Best For | Characteristics | Source |
|------|----------|-----------------|--------|
| **Inter** | All-purpose, UI, body text | Highly legible, neutral, excellent at small sizes | Google Fonts (free) |
| **Plus Jakarta Sans** | Friendly modern brands | Slightly warmer than Inter, geometric | Google Fonts (free) |
| **DM Sans** | Clean, geometric needs | Geometric, low contrast | Google Fonts (free) |
| **Space Grotesk** | Tech/innovation brands | Distinctive, geometric, futuristic feel | Google Fonts (free) |
| **Outfit** | Modern startups | Clean, approachable, wide range of weights | Google Fonts (free) |

### Professional/Corporate

| Font | Best For | Characteristics | Source |
|------|----------|-----------------|--------|
| **Source Sans Pro** | Enterprise, readable long-form | Adobe's workhorse, very neutral | Google Fonts (free) |
| **IBM Plex Sans** | Tech/enterprise | Designed for IBM, highly legible | Google Fonts (free) |
| **Work Sans** | Professional contexts | Optimized for screen, grotesque style | Google Fonts (free) |
| **Nunito Sans** | Approachable professional | Softer, friendly but professional | Google Fonts (free) |

### Premium/Sophisticated

| Font | Best For | Characteristics | Source |
|------|----------|-----------------|--------|
| **Cormorant** | Luxury, editorial | Elegant serif with display qualities | Google Fonts (free) |
| **Playfair Display** | Premium headings | High contrast, sophisticated serif | Google Fonts (free) |
| **Libre Baskerville** | Classic, trusted brands | Traditional serif, very readable | Google Fonts (free) |
| **Fraunces** | Distinctive premium | Soft serif with personality | Google Fonts (free) |

### Friendly/Approachable

| Font | Best For | Characteristics | Source |
|------|----------|-----------------|--------|
| **Poppins** | Consumer brands, apps | Geometric, friendly, popular | Google Fonts (free) |
| **Nunito** | Warm, approachable | Rounded terminals, soft | Google Fonts (free) |
| **Quicksand** | Playful, light brands | Rounded, geometric, modern | Google Fonts (free) |
| **Rubik** | Tech-friendly, modern | Slightly rounded corners | Google Fonts (free) |

### Bold/Impactful (Headlines)

| Font | Best For | Characteristics | Source |
|------|----------|-----------------|--------|
| **Oswald** | Strong headlines | Condensed, impactful | Google Fonts (free) |
| **Bebas Neue** | Display, posters | All caps, bold | Google Fonts (free) |
| **Anton** | Maximum impact | Ultra bold, condensed | Google Fonts (free) |
| **Syne** | Creative, unique | Variable width, distinctive | Google Fonts (free) |

---

## Font Pairings

### Safe Pairings (Same Family)

The easiest approach—use one font family with varied weights:

```
Headlines: Inter Bold (700)
Body: Inter Regular (400)
Captions: Inter Medium (500)
```

**Best single-family fonts for this:**
- Inter (excellent weight range)
- Plus Jakarta Sans
- IBM Plex Sans
- Source Sans Pro

### Classic Pairings (Serif + Sans)

| Heading | Body | Vibe |
|---------|------|------|
| Playfair Display | Source Sans Pro | Premium, editorial |
| Cormorant | Proza Libre | Elegant, sophisticated |
| Libre Baskerville | Open Sans | Traditional, trustworthy |
| Fraunces | Inter | Modern premium |

### Modern Pairings (Sans + Sans)

| Heading | Body | Vibe |
|---------|------|------|
| Space Grotesk | Inter | Tech, innovative |
| Syne | DM Sans | Creative, bold |
| Outfit | Source Sans Pro | Modern professional |
| Plus Jakarta Sans | Inter | Warm, approachable tech |

### Display Pairings (Impact + Readable)

| Heading | Body | Vibe |
|---------|------|------|
| Bebas Neue | Source Sans Pro | Bold, striking |
| Oswald | Nunito Sans | Strong, friendly |
| Anton | Work Sans | Maximum impact |

---

## Type Scale Systems

### Simple Scale (Startups)

```css
:root {
  --text-sm: 0.875rem;   /* 14px - captions */
  --text-base: 1rem;     /* 16px - body */
  --text-lg: 1.25rem;    /* 20px - large body */
  --text-xl: 1.5rem;     /* 24px - H3 */
  --text-2xl: 2rem;      /* 32px - H2 */
  --text-3xl: 2.5rem;    /* 40px - H1 */
  --text-4xl: 3rem;      /* 48px - display */
}
```

### Detailed Scale (Full Implementation)

```css
:root {
  /* Font sizes */
  --text-xs: 0.75rem;    /* 12px */
  --text-sm: 0.875rem;   /* 14px */
  --text-base: 1rem;     /* 16px */
  --text-lg: 1.125rem;   /* 18px */
  --text-xl: 1.25rem;    /* 20px */
  --text-2xl: 1.5rem;    /* 24px */
  --text-3xl: 1.875rem;  /* 30px */
  --text-4xl: 2.25rem;   /* 36px */
  --text-5xl: 3rem;      /* 48px */
  --text-6xl: 3.75rem;   /* 60px */
  
  /* Line heights */
  --leading-none: 1;
  --leading-tight: 1.1;
  --leading-snug: 1.25;
  --leading-normal: 1.5;
  --leading-relaxed: 1.625;
  --leading-loose: 2;
  
  /* Letter spacing */
  --tracking-tight: -0.025em;
  --tracking-normal: 0;
  --tracking-wide: 0.025em;
}
```

### Modular Scale (Mathematical)

Based on ratio 1.25 (Major Third):

```
12px → 15px → 18.75px → 23.44px → 29.30px → 36.62px → 45.78px
```

Based on ratio 1.333 (Perfect Fourth):

```
12px → 16px → 21.33px → 28.43px → 37.90px → 50.52px → 67.34px
```

---

## Font Weights

### Standard Weight Names

| Weight | Name | Use |
|--------|------|-----|
| 100 | Thin | Rarely—large display only |
| 200 | Extra Light | Large display only |
| 300 | Light | Large text, not body |
| 400 | Regular | Body text, default |
| 500 | Medium | UI elements, emphasis |
| 600 | SemiBold | Subheadings, buttons |
| 700 | Bold | Headlines, strong emphasis |
| 800 | Extra Bold | Display, maximum emphasis |
| 900 | Black | Display only |

### Recommended Weight Sets

**Minimum (3 weights):**
- 400 (Regular) - body
- 600 (SemiBold) - headings, buttons
- 700 (Bold) - emphasis, headlines

**Standard (4 weights):**
- 400 (Regular)
- 500 (Medium)
- 600 (SemiBold)
- 700 (Bold)

---

## Implementation

### Google Fonts Import

```html
<!-- HTML head -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

```css
/* CSS @import (slower, use HTML link preferred) */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
```

### CSS Font Stack

Always include fallbacks:

```css
body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
```

### Font Loading Strategy

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

For better performance:
```html
<link rel="preload" as="style" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap">
```

---

## Typography Rules (Include in Every Guide)

1. **Hierarchy**: Establish clear visual hierarchy with size and weight
2. **Line height**: 1.5-1.6 for body text, tighter (1.1-1.25) for headlines
3. **Line length**: 65-75 characters max for readability
4. **Weights**: Never use weights below 400 for body text
5. **Consistency**: Limit to 2-3 sizes per design
6. **Contrast**: Ensure text meets WCAG contrast requirements