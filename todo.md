# TODO — Shopify Skeleton Theme + Vite (Post Pre-Core)

## 0) Status
- [x] Pre-core architecture baseline completed
- [x] Vite + Shopify integration stabilized
- [x] TS entrypoints structure finalized (`frontend/entrypoints/css` + `frontend/entrypoints/ts`)
- [x] Branch-linked deploy workflow documented
- [x] README and CLAUDE docs updated

---

## 1) Repository Hygiene (final pass before core features)
- [x] Review tracked/untracked files and confirm what must be committed
- [x] Confirm `.claude/` policy (team-shared vs local-only)
- [x] Confirm `.agents/` policy (likely local-only)
- [x] Ensure `.env` and `shopify.theme.toml` are ignored
- [x] Ensure only `.env.example` and `example.shopify.theme.toml` are committed

Acceptance:
- [x] Working tree clean and intentional
- [x] No sensitive/local files tracked

---

## 2) Quality Gates & CI
- [x] Verify CI runs: `typecheck`, `vite:build`, `theme-check`
- [x] Confirm CI runs on `push` + `pull_request`
- [x] Confirm no regressions in workflow after simplifications

Step 2 closure checklist:
- [x] Open a recent PR and confirm both checks are green:
  - `Typecheck and Build`
  - `Theme Check`
- [x] Enable branch protection on `main` and `staging` with required checks:
  - `Typecheck and Build`
  - `Theme Check`
- [x] Block merge when checks are pending/failing
- [ ] (Optional) Disable direct push to `main`

Acceptance:
- [x] All checks green on PR
- [x] Failing checks block merge

---

## 3) Dev/Build Workflow Consistency
- [x] Verify `bun run dev` (local) works consistently
- [x] Verify `bun run dev:remote` works for Shopify-domain preview (tunnel)
- [x] Verify `bun run build` generates all expected assets and `vite-tag` mappings
- [x] Confirm team uses full domain in `.env` (`*.myshopify.com`)

Acceptance:
- [x] Local + remote preview both reliable
- [x] No CORS/PNA blockers in normal flow

---

## 4) Block 3 — Core Features Rollout

### Phase 1 — PDP (Product)
- [ ] Audit current PDP markup and data attributes
- [ ] Implement variant selection state logic in `ts/product.ts`
- [ ] Sync selected variant with URL and form inputs
- [ ] Update price/media state on variant change (if media mapping exists)
- [ ] Add add-to-cart UX states (loading, success, error)
- [ ] Handle unavailable / sold-out variants correctly

Acceptance:
- [ ] Variant change updates UI correctly
- [ ] Add-to-cart works and shows clear status
- [ ] No JS leakage outside PDP

### Phase 2 — Collection (PLP)
- [ ] Implement sort behavior
- [ ] Implement filters (base behavior first)
- [ ] Add optional progressive loading only if needed

Acceptance:
- [ ] Filters/sort stable and reversible
- [ ] PLP JS isolated to collection templates

### Phase 3 — Cart / Drawer
- [ ] Implement drawer open/close and focus handling
- [ ] Quantity update/remove flows with loading states
- [ ] Empty cart state UX
- [ ] Error handling and resilience

Acceptance:
- [ ] Keyboard accessible drawer behavior
- [ ] Cart updates reliable with clear feedback

### Phase 4 — Search
- [ ] Implement predictive search UI state
- [ ] Implement results state handling
- [ ] Graceful fallback when predictive endpoint unavailable

Acceptance:
- [ ] Search interactions stable
- [ ] No cross-template JS side effects

---

## 5) Performance & Loading Validation
- [ ] Capture baseline metrics (Home, PDP, PLP): LCP, CLS, JS payload
- [ ] Verify each template loads only `ts/theme.ts` + its own entrypoint
- [ ] Add dynamic imports for heavy optional logic where useful

Acceptance:
- [ ] No regressions vs baseline
- [ ] Template-specific payload discipline maintained

---

## 6) Documentation Finalization
- [ ] Keep README aligned with actual scripts and branch-linked workflow
- [ ] Keep CLAUDE.md aligned with architecture and conventions
- [ ] Add short “how to start new feature branch” section (optional)

Acceptance:
- [ ] New team member can run project in <10 minutes

---

## 7) Git/Release Workflow
- [ ] Enforce branch model: `feat/* -> staging -> main`
- [ ] Before merging to `staging`/`main`, always run `bun run build`
- [ ] Commit generated artifacts for branch-linked Shopify themes

Acceptance:
- [ ] Shopify branch previews always reflect latest built assets

---

## 8) Nice-to-have (after core)
- [ ] Add import alias usage examples (`@ts`, `@css`) in code/docs
- [ ] Add lightweight linting strategy for TS/Liquid (if needed)
- [ ] Add automated smoke checklist script (optional)
