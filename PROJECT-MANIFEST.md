# Public Good App - Project Manifest

**Repository**: https://github.com/Rothschad/Novi-AI-Projects.git  
**Last Updated**: 2026-06-24  
**Status**: ✓ Synced locally and on GitHub  
**Local Path**: `/Users/cillianburns/Desktop/Novi AI Projects`

---

## Project Files

### Core Documentation

#### 1. **DESIGN.md** (183 KB)
Complete project specification including:
- Project overview (Madrid Green Initiative)
- User flows (public, admin, council)
- Core features (MVP Phase 1 + Phase 2)
- Data model with JSON examples
- Technical architecture (React Native, Express, Firebase)
- Sample questions for 3 Madrid districts (Salamanca, Malasaña, Retiro)
- Implementation phases with detailed steps (8-32 hours each)
- Developer guidelines (code quality, performance, privacy)
- Success criteria and constraints

**When to use**: Reference for entire project scope and architecture

---

#### 2. **README.md** (19 bytes)
Project title and identifier

---

### Skills & Frameworks

#### 3. **SKILLS-ANTHROPIC.md** (4.7 KB)
Anthropic Skills Framework reference:
- What skills are and how they work
- Skill structure (SKILL.md format)
- Best practices for creating skills
- Key principles (repeatability, modularity, clarity, actionability)
- How to apply skills to Public Good app

**When to use**: Creating reusable task patterns

---

#### 4. **SKILLS-SUPERPOWERS.md** (6.6 KB)
Superpowers agentic development methodology:
- 5-stage workflow (Brainstorm → Plan → Implement → Test → Review)
- Test-Driven Development (TDD) patterns
- Red-Green-Refactor cycles
- Task breakdown strategies (2-5 hour atomic tasks)
- Code review checklists
- Comparison with other methodologies

**When to use**: Overall development process and workflow

---

#### 5. **SKILLS-HYPERFRAMES.md** (10 KB)
HyperFrames HTML-to-video rendering framework:
- What it does (HTML → MP4 video conversion)
- Key features (HTML-native, deterministic, agent-friendly)
- Animation support (GSAP, CSS, Lottie, Three.js)
- Rendering options (local CLI, Docker, AWS Lambda)
- Component library (transitions, charts, effects)
- Use cases for Public Good app (campaign videos, progress visualizations)

**When to use**: Auto-generating video content from data

---

#### 6. **SKILLS-INSTALLED.md** (298 KB)
Comprehensive documentation of all 91 installed agent skills:

**Collections:**
- Superpowers (6 skills) - Development methodology
- Context Engineering (10 skills) - Multi-agent optimization
- Marketing (45 skills) - Growth, CRO, copywriting, SEO, ads
- Anthropic (18 skills) - Document handling, design, creative
- Other (12 skills) - Utilities and tools

**Key skills by use case:**
- Development: `/brainstorming`, `/test-driven-development`, `/writing-plans`
- Marketing: `/cro`, `/copywriting`, `/seo-audit`, `/social`
- Documents: `/docx`, `/pdf`, `/pptx`, `/xlsx`
- Multi-agent: `/multi-agent-patterns`, `/context-optimization`

**When to use**: Reference for available skills and how to activate them

---

### Application Code

#### 7. **server.js** (804 bytes)
Basic Node.js server file (existing project file)

---

#### 8. **worldcup-live.html** (8.3 KB)
Existing project HTML file

---

### Hidden Directories

#### 9. **.agents/skills/** (693 files, 177 MB)
All 91 installed agent skills with full content:
- Each skill folder contains SKILL.md + references + scripts + examples
- Organized by skill name (alphabetically)
- Ready for Claude Code and other AI agents to use

**Location**: `.agents/skills/`  
**Access**: Show hidden files (Cmd+Shift+.)

---

#### 10. **.claude/skills/** (Symlink)
Symbolic link to `.agents/skills/` for Claude Code compatibility

---

#### 11. **.git/**
Git repository with full history:
- 6 commits total
- All files tracked and synced with GitHub

---

## Project Structure

```
Novi AI Projects/
├── README.md                    # Project title
├── DESIGN.md                    # Full specification (183 KB)
├── SKILLS-ANTHROPIC.md          # Anthropic skills framework
├── SKILLS-SUPERPOWERS.md        # Development methodology
├── SKILLS-HYPERFRAMES.md        # Video generation framework
├── SKILLS-INSTALLED.md          # All 91 skills reference
├── PROJECT-MANIFEST.md          # This file
├── server.js                    # Node.js server
├── worldcup-live.html          # Existing HTML
├── .git/                        # Git repository
├── .agents/
│   └── skills/                 # 91 installed agent skills
│       ├── ab-testing/
│       ├── brainstorming/
│       ├── copywriting/
│       ├── cro/
│       ├── docx/
│       ├── test-driven-development/
│       └── ... (85 more skills)
└── .claude/
    └── skills/                 # Symlink to .agents/skills
```

---

## What's Stored Locally

### Documentation (3 files)
✓ DESIGN.md - Complete project specification  
✓ SKILLS-SUPERPOWERS.md - Development methodology  
✓ SKILLS-HYPERFRAMES.md - Video framework guide  

### Framework References (3 files)
✓ SKILLS-ANTHROPIC.md - Anthropic skills framework  
✓ SKILLS-INSTALLED.md - All 91 installed skills  
✓ PROJECT-MANIFEST.md - This inventory  

### Agent Skills (91 directories)
✓ Superpowers (6) - brainstorming, test-driven-development, writing-plans, etc.  
✓ Context Engineering (10) - context-optimization, multi-agent-patterns, memory-systems, etc.  
✓ Marketing (45) - cro, copywriting, seo-audit, ads, social, emails, etc.  
✓ Anthropic (18) - docx, pdf, pptx, xlsx, mcp-builder, video, etc.  
✓ Other (12) - Various utilities and tools  

### Application Code (2 files)
✓ server.js - Node.js backend  
✓ worldcup-live.html - Frontend HTML  

---

## What's on GitHub

**Repository**: https://github.com/Rothschad/Novi-AI-Projects.git  
**Branch**: main  
**Status**: All files synced and committed  
**Size**: ~177 MB (mostly agent skills)

**Commits**:
1. first commit - Initial project setup (README.md, server.js, worldcup-live.html)
2. Add initial design document - DESIGN.md
3. Add comprehensive skills framework documentation - SKILLS-ANTHROPIC.md, SKILLS-SUPERPOWERS.md
4. Add HyperFrames - SKILLS-HYPERFRAMES.md
5. Install 91 agent skills - .agents/skills/* (693 files)
6. Add comprehensive skills installation documentation - SKILLS-INSTALLED.md

---

## How to Access Locally

### View Files
```bash
cd "/Users/cillianburns/Desktop/Novi AI Projects"
ls -la                          # View all files
ls -la .agents/skills           # View installed skills
cat DESIGN.md                   # Read specifications
```

### View Hidden Files (Finder)
1. Press `Cmd + Shift + .`
2. Navigate to project folder
3. See `.agents/` and `.claude/` directories

### Update from GitHub
```bash
cd "/Users/cillianburns/Desktop/Novi AI Projects"
git pull origin main
```

### View on GitHub
- Browse: https://github.com/Rothschad/Novi-AI-Projects
- Clone fresh: `git clone https://github.com/Rothschad/Novi-AI-Projects.git`
- Download ZIP: https://github.com/Rothschad/Novi-AI-Projects/archive/refs/heads/main.zip

---

## Next Steps

### Development Ready
✓ Project specification (DESIGN.md) complete  
✓ Development methodology documented (Superpowers)  
✓ 91 agent skills installed and ready to use  
✓ All files synced to GitHub  
✓ Git repository initialized and tracking changes  

### Ready to Build
1. Follow Superpowers methodology for development
2. Use agent skills for specialized tasks
3. Reference DESIGN.md for specifications
4. Commit code changes to GitHub

---

## Key Files to Reference

| Task | File |
|------|------|
| **Project Spec** | DESIGN.md |
| **Development Process** | SKILLS-SUPERPOWERS.md |
| **Available Skills** | SKILLS-INSTALLED.md |
| **Create Patterns** | SKILLS-ANTHROPIC.md |
| **Video Generation** | SKILLS-HYPERFRAMES.md |
| **Skill Descriptions** | `.agents/skills/[skill-name]/SKILL.md` |

---

## Statistics

- **Total project files**: 700+
- **Documentation files**: 6
- **Agent skills**: 91
- **Skill folders**: 91
- **SKILL.md files**: 91
- **Lines of documentation**: 5,000+
- **Repository commits**: 6
- **GitHub status**: Synced

---

## Files Location Cheat Sheet

```
Local:
/Users/cillianburns/Desktop/Novi AI Projects/DESIGN.md
/Users/cillianburns/Desktop/Novi AI Projects/.agents/skills/
/Users/cillianburns/Desktop/Novi AI Projects/.agents/skills/brainstorming/SKILL.md

GitHub:
https://github.com/Rothschad/Novi-AI-Projects/blob/main/DESIGN.md
https://github.com/Rothschad/Novi-AI-Projects/tree/main/.agents/skills
```

---

All files are stored locally and synced with GitHub. Ready to begin development!
