---
name: brand-guide-generator
description: Generate comprehensive brand guidelines (inspired by Avalara's Skylab design system) for any company. Use when asked to create brand guides, style guides, brand books, design systems, or visual identity documentation. Produces professional, modular brand documentation covering logo, colors, typography, voice & tone, and visual standards.
---

# Brand Guide Generator

Generate professional brand guidelines for any company—from early-stage startups to established enterprises.

## Workflow

### Step 1: Gather Brand Inputs

Before generating, collect these inputs (ask user if not provided):

**Required:**
- Company name and website URL
- Logo files (or describe if unavailable)
- Primary brand color (HEX) or let user confirm extracted color

**Optional (enhance quality if available):**
- Existing brand assets or style references
- Mission/vision statements
- Target audience description
- Competitor brands to differentiate from
- Tone preferences (formal/casual, technical/accessible)

### Step 2: Extract Brand Intelligence

If website URL provided:
1. Fetch the website to extract existing visual identity
2. Identify: primary colors, typography, tone of voice, imagery style
3. Note any inconsistencies to address in the guide

If starting from scratch:
1. Confirm brand personality with user (see `references/brand-personality.md`)
2. Recommend color palette based on industry and positioning
3. Suggest typography pairings

### Step 3: Generate Brand Guide

Output a complete brand guide document with these sections (see `references/section-templates.md` for detailed templates):

1. **Brand Overview** - Mission, vision, personality, promise
2. **Logo** - Usage rules, clear space, minimum sizes, don'ts
3. **Color Palette** - Primary, secondary, semantic colors with all values
4. **Typography** - Typefaces, scale, weights, usage rules
5. **Voice & Tone** - Principles, examples, context variations
6. **Visual Identity** - Imagery, icons, spacing, components
7. **Applications** - Email signatures, presentations, documents
8. **Quick Reference** - One-page summary card

### Step 4: Produce Deliverables

Generate these outputs:
1. **Primary document** - Full brand guide (Markdown, can convert to PDF/PPTX)
2. **Quick reference card** - One-page summary for daily use
3. **Color palette file** - CSS variables + design token formats

## Output Format

Use the structure in `references/section-templates.md` for consistent, professional output.

Key formatting rules:
- Use tables for color palettes and type scales
- Include do's and don'ts with ✅ and ❌ markers
- Provide code snippets for developers (CSS, font imports)
- Show concrete examples for voice & tone guidelines

## Customization by Company Stage

**Startup (seed/early):**
- Keep it lean: 8-12 pages
- Focus on: logo, colors, typography, basic voice
- Skip: detailed component specs, extensive applications

**Growth stage:**
- Moderate depth: 15-25 pages
- Add: messaging framework, social templates, presentation guides
- Include: basic component patterns

**Enterprise:**
- Comprehensive: 30+ pages
- Full coverage: all sections with detailed specifications
- Add: accessibility standards, localization notes, governance

## Quality Checklist

Before delivering, verify:
- [ ] All color values include HEX, RGB, and usage context
- [ ] Typography includes web-safe fallbacks
- [ ] Voice guidelines have concrete do/don't examples
- [ ] Logo rules cover common misuse scenarios
- [ ] Quick reference card is genuinely usable standalone
