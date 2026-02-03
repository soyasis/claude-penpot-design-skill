# Penpot Design Skill for Claude Code

A comprehensive Claude Code skill for creating, editing, and manipulating designs in Penpot using the connected MCP plugin. Transform your design workflow with AI-powered design automation.

## Overview

This skill enables Claude Code to work directly with Penpot designs through the Penpot MCP Plugin. Create professional UI components, manipulate layouts, generate design systems, and even convert designs to production code - all through natural language commands.

## Features

- **Create & Manipulate Shapes**: Rectangles, ellipses, text, paths, and complex vector graphics
- **Layout Systems**: Flex layouts with full control over alignment, spacing, and responsive behavior
- **Component Design**: Build reusable design components and manage design libraries
- **Styling**: Complete control over fills, gradients, strokes, shadows, and effects
- **Design-to-Code**: Generate CSS and HTML/SVG directly from your designs
- **Visual Inspection**: Export shapes for verification during the design process

## Prerequisites

You must have the **[Penpot MCP Plugin](https://github.com/penpot/penpot-mcp)** installed and connected to your Penpot project.

### Installing Penpot MCP Plugin

Follow the [Penpot MCP Plugin documentation](https://github.com/penpot/penpot-mcp) for installation instructions. The plugin enables Claude Code to interact with Penpot's design API through the Model Context Protocol.

## Installation

### Option 1: Via Skills Installer (Recommended)

Once this skill is added to the claude-plugins registry:

```bash
npx skills-installer install @soyasis/claude-penpot-design-skill/penpot-design
```

### Option 2: Manual Installation

1. Clone or download this repository
2. Copy the `penpot-design.skill` file to:
   - **Global**: `~/.claude/skills/`
   - **Project**: `./.claude/skills/` (in your project root)

### Option 3: From .skill File

Download the `penpot-design.skill` file and install it in Claude Code:

1. Open Claude Code
2. Navigate to Settings > Skills
3. Click "Install Skill" and select the `.skill` file

## Compatible Skills

Enhance your design workflow by combining this skill with other complementary skills:

- **[Frontend Design](https://claude-plugins.dev/skills/@anthropics/claude-code/frontend-design)** - Create distinctive, production-grade frontend interfaces with high design quality

  ```bash
  npx skills-installer install @anthropics/claude-code/frontend-design
  ```

Use these skills together to design in Penpot and implement directly in code, or vice versa!

## Quick Start

Once installed, the skill activates automatically when you:

- Mention "Penpot" in your conversation
- Ask Claude to create or manipulate designs
- Request design-to-code conversions
- Work with UI components and layouts

### Example Commands

```
Create a modern card component in Penpot with a title, description, and button

Design a navigation bar with a logo and menu items

Generate CSS from the selected design element

Convert this design to HTML and CSS code
```

## Documentation

- **[SKILL.md](SKILL.md)** - Complete skill reference with all APIs and patterns
- **[patterns.md](patterns.md)** - Reusable design patterns and examples
- **[api-quick-ref.md](api-quick-ref.md)** - Quick API reference guide

## Key Capabilities

### Shape Creation
Create any Penpot shape type: rectangles, ellipses, text, paths, boards (frames), and more.

### Layout Management
Build complex layouts with flex layout support, including alignment, spacing, padding, and responsive behavior.

### Component Systems
Access and create library components, manage design tokens, and build reusable design systems.

### Design-to-Code
Generate production-ready CSS, HTML, and SVG directly from your designs with `penpot.generateStyle()` and `penpot.generateMarkup()`.

### Visual Design Tools
Complete styling control including:
- Solid colors and gradients
- Strokes and borders
- Shadows and effects
- Border radius
- Typography
- Opacity and blend modes

## Critical Features

### Child Ordering in Flex Layouts
For flex layouts (`dir="column"` or `dir="row"`), the children array order is **reversed** relative to visual order. The skill handles this automatically.

### Position Management
Use `penpotUtils.setParentXY(shape, x, y)` for relative positioning, as `parentX` and `parentY` are read-only properties.

### Text Sizing
Text size is controlled via `fontSize` property, not `resize()`. Always set `growType = 'auto-width'` after resize for proper text auto-sizing.

## Examples

### Creating a Card Component

```javascript
// Claude automatically generates this via the skill:
const card = penpot.createBoard();
card.name = 'Card Component';
card.resize(300, 200);

const background = penpot.createRectangle();
background.resize(300, 200);
background.fills = [{ fillColor: '#FFFFFF' }];
background.borderRadius = 12;

const title = penpot.createText('Card Title');
title.fontSize = '20';
title.fontWeight = '600';

card.insertChild(0, background);
card.insertChild(1, title);
```

### Generating CSS from Design

```javascript
// Select elements in Penpot, then:
const css = penpot.generateStyle(penpot.selection, {
  type: 'css',
  withPrelude: true,
  includeChildren: true
});
```

## API Access

The skill provides access to:

- **`penpot`** - Main API object for selection, root, library, fonts, viewport
- **`penpotUtils`** - Helper functions for finding shapes, structure analysis, positioning
- **`storage`** - Persistent storage across tool calls

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

### Development

1. Fork the repository
2. Make your changes to `SKILL.md` or reference files
3. Test thoroughly with Penpot MCP Plugin
4. Submit a pull request

## Support

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/soyasis/claude-penpot-design-skill/issues)
- **Penpot MCP Plugin**: [https://github.com/penpot/penpot-mcp](https://github.com/penpot/penpot-mcp)
- **Documentation**: See [SKILL.md](SKILL.md) for complete reference
- **Examples**: Check [patterns.md](patterns.md) for working code examples

## License

MIT License - See [LICENSE](LICENSE) file for details

## Credits

Created for use with [Claude Code](https://code.claude.com/) and [Penpot](https://penpot.app/).

Part of the [claude-plugins](https://github.com/Kamalnrf/claude-plugins) ecosystem.

---

**Sources:**
- [Claude Plugins Registry](https://github.com/Kamalnrf/claude-plugins)
- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills)
- [CC Marketplace Example](https://github.com/ananddtyagi/cc-marketplace)
