# CAD Automation Skill Pack

Control AutoCAD, SolidWorks, Fusion 360, and FreeCAD via Claude Code skills.

## Why CADStack?

**The problem:** CAD tools require precise commands. Want a 10mm hole? You need to know the exact API call, parameter order, and coordinate system.

**The solution:** Describe what you want in natural language. CADStack generates the CAD script, validates it for safety, executes it, and verifies the output.

```
Traditional CAD:                    CADStack:
─────────────────────────────────    ─────────────────────────────────
1. Open CAD software                1. /cad "bracket with 4 holes"
2. Create sketch                      → Generated script
3. Draw rectangle                      → Safety validated
4. Add dimensions                      → Executed
5. Extrude                             → Dimensions verified
6. Create hole sketch                2. ✓ Done
7. Draw circle
8. Cut extrude
9. Repeat 3 more times
10. Export STEP
```

**What makes CADStack different:**
- **Safety-first**: Every script reviewed before execution
- **Multi-backend**: Same commands work across FreeCAD, AutoCAD, SolidWorks, Fusion 360
- **Verification built-in**: `/cad-qa` confirms dimensions match your intent
- **Headless mode**: FreeCAD works without opening a GUI

## Available Skills

| Skill | Description |
|-------|-------------|
| `/cad` | **Primary skill** — Execute CAD commands: create, modify, export parts |
| `/cad-plan` | Plan complex multi-step CAD operations before execution |
| `/cad-review` | Review generated CAD scripts for safety/correctness |
| `/cad-qa` | Verify exported files, check dimensions, validate geometry |
| `/cad-config` | Set up and configure CAD backend connections |

### Which Skill to Use

```
CADSTACK DECISION TREE

START
  │
  ▼
"Is this your first time?" ──YES──► /cad-config
  │                                (detect & configure)
  NO
  │
  ▼
"Simple operation?" ──YES──► /cad
  (single part, 1-3 steps)       (create, modify, export)
  │
  NO
  │
  ▼
"Multi-step or assembly?" ──► /cad-plan ──► /cad
                                 (plan first)   (execute)

AFTER /cad:
  • Need to verify output? ──► /cad-qa
  • Review script safety?  ──► /cad-review
```

**Quick reference:**
- **Just want to make a part?** → `/cad`
- **Building something complex?** → `/cad-plan` then `/cad`
- **Not sure it worked?** → `/cad-qa`
- **Setting up for the first time?** → `/cad-config`

## Supported Platforms

- **FreeCAD** (Recommended) - Pure Python, headless mode, no license required
- **AutoCAD** - Requires AutoCAD running, uses COM automation
- **SolidWorks** - Requires SolidWorks running, uses COM automation
- **Fusion 360** - Requires Fusion 360 running with bridge add-in

## Quick Start

```bash
# Install cadstack
git clone https://github.com/user/cadstack.git ~/.claude/skills/cadstack
cd ~/.claude/skills/cadstack && ./setup
```

Then in Claude Code:
```
/cad "Create a 100x50x20mm box with 5mm filleted edges"
```

## First Run Experience

If this is your first time using cadstack, follow this sequence:

Step 1: Verify setup
- Run `/cad-config` to detect & configure CAD backends

Step 2: Hello World
- Run `/cad "create a 10mm cube"` for a simple test

Step 3: Your first real part
- Run `/cad "create a 50×30×5mm plate with four 5mm holes at corners"`

## Prerequisites

### For AutoCAD:
- AutoCAD 2014 or later must be installed
- AutoCAD must be running
- Windows operating system (for COM automation)

### For FreeCAD (Recommended):
- FreeCAD must be installed
- Python 3.x required
- Optional: headless mode for server-side operation

## Configuration

Configure CAD backend by editing `lib/config.json`:

```json
{
  "default_platform": "freecad",
  "platforms": {
    "freecad": {
      "executable_path": "C:/FreeCAD/bin/FreeCAD.exe",
      "headless": true
    },
    "autocad": {
      "version": "2024"
    }
  }
}
```

---

**Note:** This skill requires a local CAD installation (FreeCAD recommended for free usage, or AutoCAD/SolidWorks/Fusion 360 for commercial CAD).
