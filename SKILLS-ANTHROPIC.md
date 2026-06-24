# Anthropic Skills Framework

**Source**: https://github.com/anthropics/skills  
**Version**: Current

## What Are Skills?

Skills are self-contained folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. They teach Claude how to complete specific tasks in a repeatable, consistent way.

## Skill Structure (Required)

Every skill must have a folder containing a `SKILL.md` file with:

```yaml
---
name: my-skill-name
description: What this skill does and when to use it
---

# Skill Title

[Instructions]

## Examples
[Usage examples]

## Guidelines
[Best practices]
```

## Required Frontmatter
- `name`: Unique identifier (lowercase, hyphens for spaces)
- `description`: Clear description of what the skill does and when to use it

## Content Best Practices

### Instructions
- Clear, actionable steps to follow
- Written in imperative mood
- One task per instruction
- Include code examples where relevant

### Examples
- Concrete usage demonstrations
- Real-world scenarios
- Input/output pairs where applicable
- Common pitfalls and how to avoid them

### Guidelines
- Constraints and best practices
- When to use/not use the skill
- Performance considerations
- Security/privacy guidelines

### Resources
- Supporting scripts or templates
- External documentation links
- Configuration examples
- Tools and libraries needed

## Skill Categories

1. **Creative & Design** - Art, music, design, visual content generation
2. **Development & Technical** - Testing, debugging, MCP generation, code review
3. **Enterprise & Communication** - Communications templates, branding workflows
4. **Document Skills** - PDF, DOCX, PPTX, XLSX file handling
5. **Data & Analysis** - Data processing, analytics, visualization
6. **Project Management** - Planning, tracking, collaboration

## Key Principles

### 1. Repeatability
- Same skill produces consistent results across multiple uses
- Instructions are clear enough for anyone to follow
- No ambiguity about expected outputs

### 2. Modularity
- Skills are self-contained and independent
- Can be combined with other skills
- Don't assume prior knowledge outside the skill

### 3. Clarity
- Simple language, avoid jargon
- Include examples for complex steps
- Document edge cases and exceptions

### 4. Actionability
- Every instruction is something Claude can actually do
- Specify tools, parameters, and expected outputs
- Include verification steps

## Using Skills in Your Work

### Activating Skills
1. Reference skill in your prompt: "Use the X skill to..."
2. Skills activate automatically based on task context
3. Can stack multiple skills (e.g., "Use both testing and debugging skills")

### Skill Dependencies
- Some skills build on others (e.g., testing + debugging)
- Documentation shows prerequisite skills
- Installation order matters for complex skill sets

### Custom Skills
You can create custom skills for your project:
1. Create a folder with `SKILL.md`
2. Add frontmatter with name + description
3. Write clear instructions + examples
4. Test with actual work before relying on it

## Best Practices When Creating Skills

✓ **DO**:
- Write for clarity first, brevity second
- Include examples for every major step
- Specify inputs, outputs, and success criteria
- Document any required tools or permissions
- Reference other skills when appropriate
- Test your skill before declaring it complete

✗ **DON'T**:
- Assume prior knowledge outside the skill scope
- Skip examples "because it's obvious"
- Mix multiple unrelated tasks in one skill
- Use vague language like "handle appropriately"
- Create skills for one-off tasks
- Document what tools do (that's in tool docs, not skills)

## Key Resources

- [What are skills?](https://support.claude.com/en/articles/12512176-what-are-skills)
- [Creating custom skills guide](https://support.claude.com/en/articles/12512198-creating-custom-skills)
- [Agent Skills specification](http://agentskills.io)
- [Skills API Quickstart](https://docs.claude.com/en/api/skills-guide)

## Consistency Checklist

When working, check:
- ✓ Am I using repeatable, well-structured approaches?
- ✓ Are my instructions clear and actionable?
- ✓ Did I provide examples for complex tasks?
- ✓ Are my guidelines documented?
- ✓ Can someone unfamiliar with this work follow my process?

## Applying Skills to Public Good App

For this project, create/use skills for:
1. **QR Code Generation** - Consistent QR creation from questions
2. **Vote Processing** - Standardized vote submission logic
3. **Comment Handling** - Consistent private comment storage
4. **Dashboard Updates** - Real-time data refresh procedures
5. **District Data Analysis** - Scraping and analyzing Madrid data
