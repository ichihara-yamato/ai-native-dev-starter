# Review: Assets Checks

Role: Reviewer
Purpose: Verify Vite/asset changes in PRs and ensure page-specific assets are not globalized.
Inputs: Changed entries in `resources/js` / `vite.config.js` and Blade templates.
Constraints: Avoid increasing initial bundle size; prefer `@push` for page scripts.
Outputs: Checklist and remediation suggestions.
