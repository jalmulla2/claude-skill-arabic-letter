# Arabic Letter — Claude Skill

A [Claude skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) that writes formal Arabic letters and official correspondence (خطابات رسمية) in the conventional Gulf government and organizational style.

Give it a rough description in English or Arabic (who it's to, who it's from, what it's about) and it returns a complete letter in Modern Standard Arabic with:

- the addressee block, with the right honorific (السيد / السيدة / السادة + المحترم)
- the standard greeting, subject line, and closing
- an opening sentence suited to the purpose (informing, requesting, following up)
- rank-appropriate address forms (it only uses سعادتكم when the recipient's rank calls for it)
- email mode, which leaves the subject out of the body and suggests one for the subject field

## Install

**Claude Code**

```bash
git clone https://github.com/jalmulla2/claude-skill-arabic-letter.git
cp -r claude-skill-arabic-letter/arabic-letter ~/.claude/skills/
```

**Claude.ai / Claude Desktop**

Zip the `arabic-letter` folder and upload it under Settings → Capabilities → Skills.

## Usage

Just ask:

> Write a letter to the Director of HR at Al-Mustaqbal Company asking to approve two new IT positions. I'm Ahmed Al-Hassan, Head of IT.

> اكتب خطاب لمدير الشؤون المالية بخصوص تأخر صرف المستحقات

See [`arabic-letter/SKILL.md`](arabic-letter/SKILL.md) for the full set of structure and style rules.
