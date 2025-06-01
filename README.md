# Claude Code Power Pack

Advanced slash commands and workflows for Claude Code power users.

> **⚡ Experimental Tool Collection**  
> This is an experimental personal tool collection for exploring Claude Code capabilities. 
> Use as inspiration for your own implementations. No warranties - just ideas to spark creativity!

## 🚀 Quick Example

**Want to see it in action?** Here's a real example of the `/plan_review_revise` slash command:

### What I Did
*Inside a Claude Code REPL session:*
```bash
/plan_review_revise Logging infrastructure plan, using simplicity and comprehensive perspectives. Think very hard about these.
```

### How It Worked
1. **Prerequisites**: The [`logging-infrastructure-plan-v1.md`](plans/logging-infrastructure-plan-v1.md) already existed (369-line complex plan)
2. **Natural Language Parsing**: Claude parsed my input and identified 2 review perspectives + thinking budget
3. **Parallel Processing**: Claude spawned 2 concurrent subtasks:
   - **Comprehensive Review** → Found major issues, scored 2/5, recommended 90% scope reduction
   - **Simplicity Review** → Identified over-engineering, suggested incremental approach
4. **Synthesis & Revision**: Claude combined both reviews and generated a revised plan
5. **Complete Cycle**: Plan → Review → Revise → Improved plan (simplified from 9 weeks to 2 weeks)

### What It Generated
- **Comprehensive Review**: [`logging-infrastructure-plan-v1-comprehensive-review.md`](plan-reviews/logging-infrastructure-plan-v1-comprehensive-review.md)
- **Simplicity Review**: [`logging-infrastructure-plan-v1-simplicity-review.md`](plan-reviews/logging-infrastructure-plan-v1-simplicity-review.md)
- **Revised Plan**: [`logging-infrastructure-plan-v1-revised.md`](plan-reviews/logging-infrastructure-plan-v1-revised.md)

One slash command → Natural language parsing → Parallel AI analysis → Better plans. 🧠

## Documentation

- **[Complete Power User Guide](docs/slash-commands-for-power-users.md)** - Comprehensive guide from basic commands to advanced AI workflows
- **[Slash Commands Index](docs/slash_commands/)** - Directory of implemented slash commands

## Current Features

### Plan-Review-Revise Workflow
Intelligent multi-perspective analysis of software development plans with automated review and revision.

- **📖 Detailed Guide**: [Plan-Review-Revise Workflow Guide](docs/slash_commands/plan-review-revise-workflow-guide.md) - Complete usage instructions
- **⚡ Command**: `/plan_review_revise` (implemented) - See example above!
- **🔍 Review Types**: Comprehensive, Simplicity (other types planned)
- **🎯 Example Outputs**: See the [plan-reviews/](plan-reviews/) directory for real generated reviews

### Directory Structure
- `docs/` - User guides and command documentation
- `plans/` - Example implementation plans for review
- `plan-reviews/` - Generated review outputs and revisions
- `.claude/commands/` - Slash command implementations
- `.claude/prompts/` - Review perspective prompts

## 🎯 Get Started

1. **Clone this repo** into your Claude Code project
2. **Copy the slash commands** from `.claude/commands/` to your own `.claude/commands/` directory
3. **Try the example**: Run `/plan_review_revise` on your own implementation plans
4. **Customize**: Modify the prompts in `.claude/prompts/` for your specific needs

## 🙏 Credits & Inspiration

Huge thanks to **[IndyDevDan](https://www.youtube.com/@indydevdan)** and the **[just-prompt](https://github.com/disler/just-prompt)** project for being a major inspiration for this work. While the implementations here are original (particularly the named-keyword syntax and natural language parsing in slash commands), the foundational ideas and approach were heavily influenced by Dan's excellent work on AI-powered development workflows.

If you're interested in Claude Code and AI development patterns, definitely check out IndyDevDan's YouTube channel for more inspiration!

---
*Built with ❤️ for the Claude Code community. Licensed under MIT - use, modify, and share freely!*