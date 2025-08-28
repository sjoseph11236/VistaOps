## Context

_Why are we making this change? Link to any tickets/notes._

- Issue/Task: <!-- e.g. #123 or link -->

## Changes

_What changed and why? Be specific; bullets are fine._

-
-

## Screenshots / Preview (optional)

_If UI, include before/after or a link to a preview._

-

## Testing

_How did you verify this works? Exact steps & commands, plus expected results._

- Local:
  - [ ] `open web/index.html` (or `npx http-server web`)
  - [ ] Visual check: header, badges, CTA, features, footer
  - [ ] Favicon renders
- Deploy (if applicable):
  - [ ] `./deploy.sh --dry-run` succeeds
  - [ ] No unexpected `aws s3 sync` deletions
  - [ ] CloudFront invalidation created (or intentionally skipped)

## Accessibility & Quality

- [ ] Color contrast is AA+ for key text
- [ ] Headings are structured (h1→h2→h3)
- [ ] Links have discernible text & hover/focus state
- [ ] No PHI beyond first name appears anywhere

## Risks

_What could go wrong?_

-
-

## Rollback Plan

_How to recover if something breaks._

1. `git revert <commit>`
2. Re-run `./deploy.sh`
3. CloudFront: invalidate `/*`

## Checklist

- [ ] Code builds and runs locally
- [ ] Lint passes (if applicable)
- [ ] Docs/README updated (if needed)
- [ ] Security/PHI review done (first name only)
- [ ] Reviewer(s) assigned

---

**Release notes (one line):** \_
