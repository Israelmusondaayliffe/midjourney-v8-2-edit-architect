# Midjourney V8.2 Edit Architect

A production-ready agent skill for designing, diagnosing, and sequencing prompts for the Midjourney V8.2 Edit Model.

It converts a source image, optional references, and a requested visual change into paste-ready edit prompts. It is built for native instruction editing, one-to-four-image conditioning, character and object consistency, inpainting, outpainting, environment changes, retexturing, compositing, and failure recovery.

This is an independent community skill. It is not affiliated with or endorsed by Midjourney.

## Install

### Codex

```bash
npx --yes skills@latest add Israelmusondaayliffe/midjourney-v8-2-edit-architect \
  --skill midjourney-v8-2-edit-architect \
  --global \
  --agent codex \
  --yes
```

### Claude Code

```bash
npx --yes skills@latest add Israelmusondaayliffe/midjourney-v8-2-edit-architect \
  --skill midjourney-v8-2-edit-architect \
  --global \
  --agent claude-code \
  --yes
```

### Install for both

```bash
npx --yes skills@latest add Israelmusondaayliffe/midjourney-v8-2-edit-architect \
  --skill midjourney-v8-2-edit-architect \
  --global \
  --agent codex \
  --agent claude-code \
  --yes
```

Restart the relevant agent after installation so it reloads its available skills.

For a project-only installation, run the same command from the project root and remove `--global`.

## What the skill does

The skill builds every edit around four questions:

1. What is the visual anchor?
2. What is the exact change?
3. What must not drift?
4. What makes the new content belong in the image?

It then selects the safest execution route:

- a concise one-pass instruction for low-risk edits;
- an anchor-rich prompt for identity, geometry, or composition preservation;
- a cohesion-controlled prompt for light, perspective, material, grain, and style matching;
- a staged edit chain when pose, viewpoint, environment, identity, and styling compete.

Unless another format is requested, it returns four faithful routes for the same requested outcome:

1. Precision Delta
2. Anchor-Rich
3. Cohesion-Controlled
4. Production Fallback

## Example requests

```text
Use the Midjourney V8.2 Edit Architect. Replace the paper coffee cup with an antique brass hourglass. Preserve the table, camera position, reflections, warm window light, depth of field, and film grain.
```

```text
Use the woman in the first reference as the subject, the jacket in the second reference as the garment, and the alley in the third reference as the environment. Keep her face, short black curls, silver nose ring, and body proportions consistent. Give me a staged Discord workflow.
```

```text
Diagnose this failed V8.2 edit. The object is floating, the character's face changed, and the new background has a different rendering style. Revise only the controls that caused the failures.
```

## Repository structure

```text
.
├── SKILL.md
├── README.md
├── LICENSE
└── references
    ├── current-model-boundaries.md
    ├── edit-patterns.md
    └── failure-recovery.md
```

### `SKILL.md`

The operating instructions, trigger conditions, risk routing, reference architecture, parameter safety, output contract, and final verification checklist.

### `references/current-model-boundaries.md`

The dated compatibility matrix for the V8.2 Edit Model, reference types, parameters, web and Discord syntax, official capabilities, and provisional field-tested behavior.

### `references/edit-patterns.md`

Reusable edit patterns for removal, replacement, addition, reorientation, relocation, garment transfer, multi-reference composition, retexturing, inpainting, outpainting, aspect-ratio changes, and layered workflows.

### `references/failure-recovery.md`

A diagnosis and repair system for identity drift, style bleed, floating objects, wrong counts, direction errors, ignored instructions, over-editing, geometry damage, text drift, pose failures, and aspect-ratio deformation.

## Core safety rules

The skill does not treat Midjourney controls as deterministic locks. It does not promise pixel-perfect preservation or exact identity. It also prevents unsupported or misapplied controls from entering V8.2 Edit Model prompts.

In particular:

- `--sref` and `--sw` are style controls, not identity or edit-strength controls.
- `--iw` belongs to a separate Image Prompt, not an Edit Model reference.
- `--ar` changes output geometry and should be paired with explicit expansion or reframing language.
- high-risk edits should be split into passes instead of solved with an increasingly overloaded prompt.
- the rendered result must be inspected before an edit is considered successful.

## Version boundary

The skill was last verified against official Midjourney material on September 1, 2026. Product behavior can change. Refresh `references/current-model-boundaries.md` when Midjourney changes the Edit Model, reference systems, parameter compatibility, Personalization, Moodboards, HD output, inpainting, or outpainting.

## Research basis

The skill distinguishes official capabilities from dated community testing. Its current boundaries were informed by:

- [Midjourney Edit Model documentation](https://docs.midjourney.com/hc/en-us/articles/48495453462797)
- [Midjourney model version documentation](https://docs.midjourney.com/hc/en-us/articles/32199405667853-Version)
- [Midjourney Edit image-quality update](https://updates.midjourney.com/edit-image-quality-update/)
- [The open Agent Skills CLI](https://github.com/vercel-labs/skills)

## Update an installed copy

```bash
npx --yes skills@latest add Israelmusondaayliffe/midjourney-v8-2-edit-architect \
  --skill midjourney-v8-2-edit-architect \
  --global \
  --agent codex \
  --agent claude-code \
  --yes
```

Re-running the scoped install command fetches the current repository version and keeps the installation limited to this skill and the named agents.

## License

MIT. See [LICENSE](LICENSE).
