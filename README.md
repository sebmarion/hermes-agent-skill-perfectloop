# perfectloop

Hermes skill for designing recurring agent loops before scheduling them.

This repo contains one installable skill: `SKILL.md`. The skill does not run jobs by itself. It makes Hermes define the loop contract first: goal, trigger, context, actions, verifier, state, budget, stop condition, and cleanup.

Use it when the failure mode would otherwise be "an agent keeps trying forever and grades its own work."

## What the skill does

When loaded, `perfectloop` pushes Hermes to:

- decide whether a loop is justified at all;
- reject vague or unfalsifiable goals;
- require an external gate such as tests, CI, API output, logs, screenshots, benchmarks, or human review;
- separate the maker from the checker;
- define persistent state so each run knows what already happened;
- set retry, budget, permission, and stop limits;
- specify how scheduled jobs are paused, removed, or verified as cleaned up.

The expected output is a loop spec, not a cron job pasted on vibes.

## When to use it

Good fit:

- recurring repo maintenance;
- watchdogs and monitors;
- scheduled research or triage;
- autonomous coding routines;
- repeated QA checks;
- any workflow where a bad loop could waste tokens, mutate the wrong thing, or keep running after it should stop.

Bad fit:

- one-off work;
- pure taste or strategy calls;
- tasks with no independent verifier;
- anything where the agent would be both author and judge.

## Install

Clone the repo:

```bash
git clone https://github.com/sebmarion/hermes-agent-skill-perfectloop.git
cd hermes-agent-skill-perfectloop
```

Install into your default Hermes profile:

```bash
mkdir -p ~/.hermes/skills/software-development/perfectloop
cp SKILL.md ~/.hermes/skills/software-development/perfectloop/SKILL.md
```

Start a fresh Hermes session and load it:

```bash
hermes -s perfectloop
```

Or install from the raw file:

```bash
hermes skills inspect https://raw.githubusercontent.com/sebmarion/hermes-agent-skill-perfectloop/main/SKILL.md
hermes skills install https://raw.githubusercontent.com/sebmarion/hermes-agent-skill-perfectloop/main/SKILL.md
```

## Example prompt

```text
Use perfectloop to design a weekly loop that reviews my repo issues, picks one low-risk improvement, implements it, verifies it, and stops if CI is red or the diff grows too large.
```

A useful answer should include:

- the falsifiable goal;
- inputs read each run;
- allowed and forbidden actions;
- maker/checker split;
- objective gates;
- persistent state path;
- retry and budget limits;
- stop, pause, and cleanup rules;
- first manual dry-run plan.

## Repository contents

- `SKILL.md`: the Hermes skill.
- `README.md`: this file.

## License

MIT
