---
description: Run a STRIDE threat model for the specified files or recent changes
argument-hint: "[files, directories, or components to analyze]"
---

Run a focused STRIDE threat model for `$ARGUMENTS`.

1. Read `docs/SECURITY_SURFACE.md` first. Use it to understand the documented assets, trust boundaries, entry points, and existing controls. If it is missing or does not cover the target, say so and base conclusions only on evidence found in the repository.
2. Select the analysis scope:
   - If arguments were provided, treat them as the requested files, directories, or components. Resolve component names to relevant code and include directly related handlers, authorization checks, storage, and configuration where needed.
   - If no arguments were provided, analyze files changed in the working tree (staged, unstaged, and untracked). If there are none, use files changed in the latest commit. State the scope selected.
3. Inspect the selected code and relevant callers/configuration. Identify concrete attack scenarios and map each to one or more STRIDE categories: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege. Do not infer a vulnerability from a category alone; report only risks supported by code or clearly label assumptions.
4. For each threat, provide:
   - STRIDE category and severity (Critical, High, Medium, or Low)
   - A concise attack scenario and the affected asset or trust boundary
   - Exact affected file path and line range(s), citing the code that creates or fails to mitigate the risk
   - A specific code mitigation, describing the validation, authorization, encoding, audit, resource limit, or other change needed. Include a small illustrative snippet when it makes the recommendation unambiguous; do not modify files unless explicitly asked.
5. If a STRIDE category has no supported threats in scope, list it under “No supported threats identified” rather than inventing a finding. Distinguish confirmed findings from assumptions and note important coverage limitations.

Use this output format:

## Scope
- Targets analyzed and how they were selected
- Relevant coverage from `docs/SECURITY_SURFACE.md`

## Threats
For each finding, use:

### [Severity] [STRIDE category] — short title
- **Scenario:** …
- **Affected:** `path/to/file.ext:line-line` — …
- **Mitigation:** …

## No supported threats identified
- List STRIDE categories with no supported findings, or state “None” if all categories have findings.

## Assumptions and limitations
- List material assumptions or say “None.”
