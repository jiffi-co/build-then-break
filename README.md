<p align="center">
  <img src="assets/banner.png" alt="Build, then break. A Claude Code skill. Build with restraint, then switch sides and try to break your own work." width="100%">
</p>

<p align="center">
  <a href="LICENSE"><img alt="Licence: MIT" src="https://img.shields.io/badge/licence-MIT-0f063c"></a>
  <img alt="Works with Claude Code" src="https://img.shields.io/badge/works%20with-Claude%20Code-599cff">
  <a href="https://github.com/jiffi-co/show-then-build"><img alt="Pairs with show-then-build" src="https://img.shields.io/badge/pairs%20with-show--then--build-d5e6ff"></a>
  <a href="https://clarityclub.jiffi.co"><img alt="From Jiffi Clarity Club" src="https://img.shields.io/badge/from-Jiffi%20Clarity%20Club-fff58a"></a>
</p>

# Build, then break

AI coding assistants have two bad habits. They build more than you asked for, and they call it done at the first green tick.

This skill fixes both. It makes Claude Code build with restraint, then switch sides and try to break its own work before it tells you anything is finished.

You don't need to be a developer to use it. You install it once and it runs in every project.

## Install it in a minute

It installs from the builder-kit-lean marketplace. In a terminal:

```bash
claude plugin marketplace add jiffi-co/builder-kit-lean
claude plugin install build-then-break@builder-kit-lean
```

To have Claude Code use it every time, add this section to `~/.claude/CLAUDE.md`:

```text
## Build, then break
For any task that writes, edits, refactors, debugs or reviews code, and before calling any plan or analysis done, use the build-then-break skill and follow it. Match effort to the stakes as the skill describes.
```

Start a fresh session afterwards. That's it.

Prefer to install it by hand, or from a zip? See [INSTALL.md](INSTALL.md).

## What changes

**Before.** You ask for a bug fix. You get the fix, a refactor you didn't ask for, new settings nobody needs, and "all tests pass".

**After.** You get the smallest change that fixes it, a test that proves it, and a short report of what the AI tried to break and what held.

A report looks like this:

> `first_even` now returns `None` when no even number exists (was `IndexError` on empty and all-odd lists; test added for both). Held: negative evens. Open: should `2.0` count? The spec doesn't say.

## How it works

It picks a level first, so a typo fix stays cheap and a payments change gets the full drill.

| Level | When | Build | Break |
|---|---|---|---|
| Trivial | Typo, rename, config value, obvious one-liner | Surgical change only | Run it. Nothing more. |
| Standard | Feature, bug fix, refactor | All four build rules | The project's tests, plus the three attacks most likely to land |
| High-stakes | Money, auth, data migrations, production deploys, security, anything hard to undo, or a plan someone will act on | All four rules, plan written as checked steps | The full drill, every relevant vector |

### Build

1. **Think first.** State the assumptions. Ask when two readings would change the outcome.
2. **Simplest thing that works.** No features, settings or abstractions nobody asked for.
3. **Surgical changes.** Touch only what the task needs. Match the existing style.
4. **A goal you can check.** "Fix the bug" becomes a test that fails, then passes.

### Break

1. **State the claim exactly.** You can't attack a vague claim.
2. **Attack where a subtle bug would hide.** Boundaries, hostile input, hidden assumptions, state, failure, scale, and what was asked against what was assumed.
3. **Force a verdict on each attack.** It survives with a reason or a test, or it breaks and gets fixed.
4. **Write the test you're slightly afraid to run.**
5. **Stop when it survives a real attack**, not at the first green tick.

It works on plans and decisions too. State the conclusion, argue the strongest opposite case properly, keep the conclusion only if it survives.

The full skill is one short file: [skills/build-then-break/SKILL.md](skills/build-then-break/SKILL.md).

## What's in the box

```text
skills/build-then-break/
├── SKILL.md                      the skill
└── references/
    ├── examples.md               each build rule, shown in code
    └── worked-example.md         a full break drill
```

No scripts. No network calls. It is instructions and examples, nothing else.

## Using it

Once it's installed with the CLAUDE.md section, you don't have to do anything. Claude Code uses it whenever it writes, edits or reviews code.

To call it yourself, say "use build-then-break on this".

## Better with show-then-build

This skill answers "is it built right?". Its partner, [show-then-build](https://github.com/jiffi-co/show-then-build), answers "what should we build?". It shows you a change on a page you can click before anything is built, then hands the build to this skill.

Show always leads into break. Break doesn't need show: a typo or a one-line fix comes straight here.

To install both, see the [show-then-build page](https://github.com/jiffi-co/show-then-build#install-it-in-a-minute).

## Credits

- Build rules adapted from [karpathy-guidelines](https://github.com/forrestchang/andrej-karpathy-skills) (MIT), which turns Andrej Karpathy's observations on LLM coding pitfalls into four rules. `references/examples.md` comes from that project.
- Break drill adapted from the adversarial-review skill in the Clarity starter pack.
- Put together by [Jake Shelley](https://github.com/jake-jiffi) at [Jiffi](https://www.jiffi.co) for [Clarity Club](https://clarityclub.jiffi.co), where we help business people build with AI properly.

## Licence

[MIT](LICENSE). Use it, change it, share it.
