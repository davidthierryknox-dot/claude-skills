# Brand Guide Generator

A skill for generating comprehensive brand guidelines for companies and products.

**Works with:** Claude | ChatGPT | Gemini

## What It Does

This skill helps create professional brand guides including:

- Brand overview (mission, vision, personality)
- Logo usage guidelines
- Color palettes with accessibility considerations
- Typography systems and font recommendations
- Voice and tone guidelines
- Visual identity standards

## Installation by Platform

### Claude

Import `brand-guide-generator.skill` into your Claude account under Capabilities/Skills.

### ChatGPT (Custom GPT)

1. Go to [ChatGPT](https://chat.openai.com) → Explore GPTs → Create
2. Follow instructions in [`chatgpt/INSTRUCTIONS.md`](./chatgpt/INSTRUCTIONS.md)
3. Upload the knowledge files from [`chatgpt/knowledge/`](./chatgpt/knowledge/)

### Gemini (Gem)

1. Go to [Gemini](https://gemini.google.com) → Gem manager → New Gem
2. Follow instructions in [`gemini/INSTRUCTIONS.md`](./gemini/INSTRUCTIONS.md)
3. Reference files available in [`gemini/references/`](./gemini/references/)

## Folder Structure

```
brand-guide-generator/
├── brand-guide-generator.skill    # Claude skill file
├── chatgpt/
│   ├── INSTRUCTIONS.md            # Setup guide for Custom GPT
│   └── knowledge/                 # Files to upload as GPT knowledge
├── gemini/
│   ├── INSTRUCTIONS.md            # Setup guide for Gem
│   └── references/                # Reference files for context
├── references/                    # Original reference materials
│   ├── brand-personality-guide.md
│   ├── color-palette-reference.md
│   ├── section-templates.md
│   └── typography.md
└── extracted/                     # Extracted .skill contents
```

## Reference Materials

| File | Description |
|------|-------------|
| `brand-personality-guide.md` | Brand personality frameworks (Aaker Model, Jungian Archetypes) |
| `color-palette-reference.md` | Color extraction, industry conventions, and palette templates |
| `typography.md` | Font recommendations, pairings, and implementation |
| `section-templates.md` | Templates for each brand guide section |

## Platform Differences

| Feature | Claude | ChatGPT | Gemini |
|---------|--------|---------|--------|
| Knowledge files | Bundled in .skill | Upload separately | Upload per-chat |
| Web browsing | Yes | Yes (enable) | Yes |
| Code generation | Yes | Yes (Code Interpreter) | Yes |
| Persistent memory | Via skill | Via GPT | Limited |
