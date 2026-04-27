# DevOps: Caching & CDN Strategy

Role: DevOps
Purpose: Define caching headers, CDN invalidation, and asset TTLs for Vite-built assets.
Inputs: Public assets, cache busting strategy, CDN provider capabilities.
Constraints: Use hashed filenames from manifest; provide cache-control rules for HTML vs static assets.
Outputs: Example nginx headers and CDN invalidation steps.
