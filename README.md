# no-slop

A Claude skill that strips the behaviors users complain about most: sycophancy, preamble, excessive hedging, unsolicited moralizing, over-structuring, closing offers, and AI tics ("delve", "let me break this down", em dashes, "I hope this helps!").

Built from recurring public feedback on where Claude feels annoying.

---

## before / after

**prompt:** `how do python generators work?`

without no-slop:
> Great question! Python generators are a really powerful feature of the language. Let me break this down for you. A generator is a special type of iterator that...

with no-slop:
> A generator is a function that produces values one at a time using `yield` instead of `return`. Each call to `next()` runs the function until the next `yield`, hands back that value, and pauses the function's state.

12 more before/after pairs in [`evals/examples.md`](evals/examples.md).

---

## install

Pick whichever fits your setup:

**Anthropic API** (recommended for most cases):
Paste the contents of [`SKILL-compact.md`](SKILL-compact.md) into your system prompt. It is 2.2kb so it will not eat your context budget.

**Claude Code**:
```bash
git clone https://github.com/iam25th1/no-slop.git ~/.claude/skills/no-slop
```

**claude.ai Projects**:
Paste the contents of [`SKILL.md`](SKILL.md) into your Project's custom instructions.

**Cursor / other IDE AI tools with system prompt config**:
Paste [`SKILL-compact.md`](SKILL-compact.md) into the system prompt field.

---

## what's in the box

| file | what it is |
|---|---|
| `SKILL.md` | full version, 16 rules with examples and a pre-send checklist, 6.8kb |
| `SKILL-compact.md` | token-tight version, 2.2kb, all 16 rules preserved |
| `evals/evals.json` | 12 test prompts in anthropic skill-creator eval schema |
| `evals/examples.md` | before/after pairs for eyeballing whether it is working |

---

## what it fixes

| complaint | rule |
|---|---|
| launching into solutions when someone was venting | 3 |
| "great question! let me break this down..." | 1, 2 |
| ending every response with "would you like me to..." | 9 |
| stacked hedges ("it's worth noting... keep in mind that...") | 5 |
| "both have merit, it depends" when asked A or B | 6 |
| agreeing with flawed premises | 7 |
| bullet lists for a conversational question | 4 |
| explaining git to someone debugging a merge conflict | 10 |
| unsolicited ethics lectures on technical questions | 13 |
| "delve", "dive into", em dashes, "I hope this helps!" | 12 |
| "I'll be concise" followed by a paragraph | 8 |
| fake hedging instead of "I don't know" | 14 |
| refusing then offering an unrelated weaker task | 15 |

---

## what it does NOT override

- Safety rules (harm, child safety, weapons, etc.)
- Explicit user instructions
- Legal or medical contexts where hedging is genuinely protective
- Creative writing where voice and flourish are the point
- Formal documents where register matters

User preferences always win.

---

## testing the skill

Run the 12 prompts from `evals/examples.md` twice, once with the skill loaded and once without. Diff the responses. If a "with skill" response still looks like the "slop" column in `examples.md`, that rule is not landing and needs sharper wording.

For the quantitative route: the JSON in `evals/evals.json` is compatible with anthropic's skill-creator eval pipeline if you want automated grading.

---

## contributing

Spotted a rule that is wrong, a tic that should be added, or a case where the skill over-corrects?

1. Fork
2. Add a failing test case to `evals/examples.md` showing the problem
3. Propose the fix (new rule, edited rule, removed rule)
4. PR

Rules that cannot be demonstrated with a before/after example probably do not belong in the skill.

---

## credit

Built by [@25thprmr](https://x.com/25thprmr) based on recurring patterns in public Claude feedback (reddit, x, HN, anthropic forums).

## license

MIT
