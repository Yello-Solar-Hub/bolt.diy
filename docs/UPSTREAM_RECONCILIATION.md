# Upstream Reconciliation Ledger

**Generated:** 2026-07-17  
**Target:** `Yello-Solar-Hub/bolt.diy`  
**Target head:** `cfca82478bbf11578b023abbeadd9d23f0515bc8`

## Purpose

Record the lineage, divergence, and explicit adoption decisions between the Yello fork and its two relevant sources:

1. **Primary upstream:** `stackblitz-labs/bolt.diy`
2. **Origin lineage:** `stackblitz/bolt.new`

This ledger prevents blind merges from treating product-specific changes as universally applicable fixes.

## Reconciliation result

| Comparison | Status | Ahead | Behind | Merge base | Decision |
|---|---:|---:|---:|---|---|
| `stackblitz-labs/bolt.diy@2e254ac` → Yello `main` | ahead | 4 | 0 | `2e254ac` | No upstream sync required |
| `stackblitz/bolt.new@eda10b1` → Yello `main` | diverged | 1534 | 2 | `cecbc55` | Review origin-only commits individually |

## Primary upstream decision

The Yello fork contains the current `stackblitz-labs/bolt.diy` head and is four commits ahead. The local changes include:

- dependency and lockfile updates;
- GitHub API route reorganization;
- centralized GitHub token handling;
- a GitHub Copilot provider;
- UI and runtime compatibility adjustments;
- test-script exclusions in `.gitignore`.

**Decision:** preserve the Yello commits. There are no missing commits from the primary upstream at the evaluated heads.

## Origin-only commit review

### `24a43b851d6e13816cc26aa1b77adc9299dac875`

**Title:** `docs: issue template links (#4066)`

Adds Bolt.new-specific support destinations:

- Bolt.new Help Center;
- Bolt.new billing support;
- StackBlitz Discord.

The Yello/bolt.diy issue configuration already routes Bolt.new problems back to `stackblitz/bolt.new` and routes bolt.diy community questions to the oTTomator Think Tank.

**Decision:** do not cherry-pick. The change is valid for the commercial Bolt.new product but would overwrite downstream-specific support routing.

### `eda10b121221b30825a4c16eec5da1fd3eb1eb99`

**Title:** `chore: bug template to suggest projects public or accessible by URL (#4222)`

Adds a mandatory project-visibility confirmation and a Bolt.new screenshot to the bug form.

The bolt.diy form has downstream-specific fields for provider and model, and its reproducibility requirements may include local deployments that cannot expose a Bolt.new project URL.

**Decision:** do not cherry-pick as-is. The reproducibility idea is useful, but any adoption should be rewritten for local/self-hosted environments and submitted as an independent change.

## Canonical source policy

- Use `stackblitz-labs/bolt.diy` as the **merge/cherry-pick upstream**.
- Use `stackblitz/bolt.new` as a **lineage and product-pattern reference**, not as a default merge source.
- Classify every origin-only commit as one of:
  - portable fix;
  - adaptable product pattern;
  - product-specific change;
  - obsolete or superseded change.
- Never import branding, billing, hosted-product support, or issue-routing changes without downstream adaptation.

## Recommended validation gate

Before merging future upstream changes into the Yello fork:

1. verify merge-base and ahead/behind counts;
2. list changed files and classify product-sensitive paths;
3. run install, lint, typecheck, tests, and production build;
4. inspect authentication, provider registry, API routes, and lockfile changes separately;
5. record accepted, adapted, and rejected commits in this ledger or a linked PR.

## Current conclusion

The Yello fork is synchronized with its primary upstream and intentionally divergent from the Bolt.new origin. No source commit should be merged during this reconciliation run.
