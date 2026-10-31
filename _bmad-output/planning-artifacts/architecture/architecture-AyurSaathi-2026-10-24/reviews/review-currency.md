# Currency review: ARCHITECTURE-SPINE.md (reviewed 2026-10-31)

Verdict: Versions and technology choices are real and current; four items are unconfirmed or wrong-by-default and need a spine edit or scaffold check.

## Confirmed (npm registry, 2026-10-31)
next 16.4.3 (= latest), react 19.3.1, typescript 7.0.2 (= latest), supabase-js 2.118.0, @supabase/ssr 0.12.7, supabase CLI 2.122.0, zod 4.6.7, tailwindcss 4.3.3, vitest 5.0.5, @playwright/test 1.64.1, @serwist/next and serwist 9.5.13. Every pinned version equals the registry latest.
- Next 16.4.3 engines node >=20.9; Node 22 LTS fine. Vitest 5.0.5 needs node ^22.12 || ^24 || >=26, so "Node 22 LTS" must mean >=22.12 (state it).
- @supabase/ssr 0.12.7 peer: supabase-js ^2.114; 2.118.0 satisfies it.
- Supabase docs: Next.js 16 renamed middleware.ts to proxy.ts; docs say getClaims is the call to use server-side, getSession must never be trusted; env var is NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY. The official with-supabase starter on canary has proxy.ts, calls getClaims in lib/supabase/proxy.ts. AD-3 and AD-4 are consistent with this.
- Custom access token hook: docs confirm it runs before token issue and can add/change claims; required claims must be kept; SQL hook needs execute granted to supabase_auth_admin and revoked from others. The fetched page did not show how policies read claims (auth.jwt()) or the refresh timing; spine's "applies at next token refresh" is consistent with the JWT model but was not confirmed from docs here.
- pg_cron: Supabase Cron is built on pg_cron, can call DB functions, sub-minute to yearly; guidance of <=8 concurrent jobs, <10 min each. Hourly job is fine. Plan availability not stated on the page.
- pgTAP: `supabase test db` documented (CI example: supabase start, then supabase test db); example layout supabase/tests/database. Spine uses supabase/tests/ (works; CLI scans supabase/tests, but not confirmed from this page).

## Findings

1. HIGH - Stack table, Serwist 9.5.13 / `Next 16` : @serwist/next is the webpack plugin path. Next 16 defaults to Turbopack, and Serwist's own docs point Turbopack users to a separate package, @serwist/turbopack (also 9.5.13, needs esbuild peer). No official statement found that @serwist/next works under Turbopack. Spine lists only "Serwist 9.5.13" and "Offline: app shell". Fix: name the package and build mode (either `@serwist/turbopack`, or `next build --webpack` with `@serwist/next`), add as an assumption, verify at scaffold; note service worker is typically disabled in dev.

2. MEDIUM - TypeScript 7.0.2 [ASSUMPTION]: version exists (dist-tag latest) and is a native-port major, but I could not confirm Next 16.4 / Zod 4 / Vitest 5 / eslint-config-next compatibility. Positives: @serwist peer typescript >=5. Negatives: the starter pins typescript ^5 and eslint-config-next (starter pins 15.3.1; latest 16.4.3), and Next type-checks with the `typescript` package API at build, which a native rewrite may not expose. Fix: keep the assumption but make the fallback the default (pin TS ^5, upgrade as a separate task) since nothing in the architecture depends on TS 7; resolve Open Question 3 now with a scaffold build.

3. MEDIUM - Tailwind and starter drift: the live starter (canary) still has tailwindcss ^3.4.1, tailwind.config.ts, postcss+autoprefixer, eslint-config-next 15.3.1, `"next": "latest"`, `"@supabase/ssr": "latest"`, radix + shadcn/ui, next-themes, lucide-react. The spine only mentions the Tailwind pin. Fix: add a "starter delta" line (replace `latest` with exact pins, bump eslint-config-next to 16.4.3, drop next-themes/radix if unused, Tailwind 4 migration changes config and postcss), and say the spine's lib layout (modules/, lib/db) replaces the starter's lib/supabase.

4. MEDIUM - AD-3 custom claims: the hook doc says the top-level `role` claim is the Postgres role (enum anon/authenticated). Spine says the hook "places `role` ... in the user's token". Overwriting top-level `role` with an app role (patient/staff) would break PostgREST role switching. Fix: state that app role and clinic_id go in `app_metadata` (or a custom claim name such as `app_role`), and `app.current_role()` reads via `auth.jwt()`; also note the function name `current_role` collides with the SQL keyword `current_role` (use `app.current_app_role()`).

5. LOW - Mumbai region, Supabase Cron plan availability, SMTP limits are correctly marked verify/open; leave. "Supabase-managed Postgres with pgTAP and pg_cron" is stated as fact; both are installable extensions (pg_cron enabled via dashboard/migration `create extension`, pgTAP only in local test DB) - phrase as "enable in migration".

## Not confirmed
Hook claim refresh timing from docs; supabase/tests path convention; Serwist on Next 16 Turbopack; TS 7 + Next 16; Vitest 5 with Next 16 / React 19.3; Supabase region list.
