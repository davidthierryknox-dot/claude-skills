# AI Skills Collection

A collection of custom skills/prompts for AI assistants, with versions for multiple platforms.

## Supported Platforms

| Platform | Feature Name | Setup |
|----------|--------------|-------|
| **Claude** | Skills | Import `.skill` file |
| **ChatGPT** | Custom GPTs | GPT Builder + knowledge files |
| **Gemini** | Gems | Gem manager |

## Skills

### Brand Guide Generator

Generate professional brand guidelines for any company—from startups to enterprises.

**Includes:**
- Brand personality frameworks (Aaker Model, Jungian Archetypes)
- Color palette recommendations by industry
- Typography guidance and font pairings
- Section templates for complete brand guides

[View Skill →](./brand-guide-generator/)

## How to Use

Each skill folder contains:

```
skill-name/
├── skill-name.skill           # Claude skill file
├── chatgpt/
│   ├── INSTRUCTIONS.md        # ChatGPT setup guide
│   └── knowledge/             # Files to upload
├── gemini/
│   ├── INSTRUCTIONS.md        # Gemini setup guide
│   └── references/            # Reference files
└── references/                # Shared reference materials
```

Pick your platform and follow the instructions in the corresponding folder.

## Contributing

To add a new skill:
1. Create a folder with the skill name
2. Add versions for each platform you support
3. Include a README with usage instructions

## License

MIT
