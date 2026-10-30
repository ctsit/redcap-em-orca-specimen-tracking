# REDCap EM review findings — `add_box_browse_review_and_edit` vs `main`

Review date: 2026-10-29. Level: medium.
Standard `/code-review` pass: 9 findings. REDCap-EM checklist pass: 5 findings.

## Standard pass (correctness / simplification / efficiency)

1. **npm scripts point at deleted vite configs** — `package.json:6` (correctness)
   The `dev-*` and `build` scripts still point at `vite.config-{config,dashboard,shipment,report}.js`, which this branch deletes.
   *Failure:* `npm run build` / `npm run dev-dashboard` fail with "config file not found", so the gitignored `dist/` can't be built. Change the scripts to `vite build` and `vite build --watch`.

2. **Modal loading Dialog undoes form focus moves** — `src/components/SpecimenForm.vue:912` (correctness)
   BlockUI was replaced with a modal PrimeVue Dialog, which traps focus while open and restores it on hide. That undoes `focusNext`/`resetFocus` during requests.
   *Failure:* After a scan, focus returns to `specimen_name` (or to Save after a save), which breaks the barcode-scanner entry flow.

3. **BoxList crashes when config/save-state is missing** — `src/components/BoxList.vue:45` (correctness)
   The template reads `config['fields']['box']` and `config['save-state']['box'][fk]` with no guards.
   *Failure:* If initialize-box-dashboard returns errors, config stays `{}` and a search throws "Cannot read properties of undefined (reading 'box')". Any box field without a save-state row also throws. Use optional chaining.

4. **New box columns show raw codes, not labels** — `src/components/BoxList.vue:48` (correctness)
   The configurable columns print the raw stored value and never map choice codes or missing-data codes.
   *Failure:* A dropdown field such as freezer shows `3` or `NASK` instead of its label. Reuse the mapping in ShipmentMain's `boxDisplayValue` or DashboardMain's `boxDisplayInfo`.

5. **Production build ships full sourcemaps** — `vite.config.js:12` (security)
   `sourcemap: true` is set in the only build config.
   *Failure:* Every install serves the full Vue source and has a larger `dist/`. Use sourcemaps only in watch/dev builds, or set them to `'hidden'`.

6. **In-app help lacks a Specimen Box List row** — `src/components/ConfigMain.vue:805` (docs)
   The Field Configurations help dialog doesn't describe the new column or which fields are required.

7. **Loading overlay Dialog duplicated in 6 components** — `src/components/DashboardMain.vue:881` (simplification)
   The same ~18-line Dialog + ProgressSpinner block appears in DashboardMain, ConfigMain, SpecimenForm, ShipmentMain, ShipmentSearch and ReportMain. Extract a `<LoadingOverlay :visible>` component.

8. **PrimeVue theme preset duplicated in 4 app.js files** — `src/pages/dashboard/app.js:19` (simplification)
   The `definePreset(Lara, …)` block is copied four times, and `darkModeSelector: false || 'none'` is just `'none'`. Move the theme setup into a shared `src/theme.js`.

9. **Dead `.overlay` CSS** — `src/components/ConfigMain.vue:905` (simplification)
   The `.overlay` rules remain in ConfigMain, DashboardMain, SpecimenForm and ShipmentMain after the element that used them was removed.

## REDCap-EM checklist pass

1. **save-module-config has no server-side rights check** — `traits/ConfigUtils.php:48` (redcap-security, pre-existing)
   `handleSaveModuleConfig` stores the whole client payload without checking user rights. `"restricted": true` only hides the menu link.
   *Failure:* Any box-project user can call the `save-module-config` ajax action and overwrite the configuration for everyone.

2. **Developer-local IDE config committed** — `.idea/deployment.xml:9` (redcap-docs)
   The branch changes the local deployment mapping, removes the upstream `github` mapping and deletes `.idea/webServers.xml`. Revert these files or drop them from the PR.

3. **2.0.7 changelog omits the build overhaul** — `CHANGELOG.md:1` (redcap-docs)
   It doesn't mention the Vite 5→8 and plugin-vue 4→6 upgrades, the switch to a single multi-entry vite config, or the BlockUI/style.scss removals.

4. **framework-version 14; current is 17** — `config.json:16` (redcap-modernization)
   v14 dates from 2023-06. v16 (2024-08) and v17 (2026-04) are current.

5. **UI strings hardcoded; no i18n** — `src/components/ConfigMain.vue:423` (redcap-modernization)
   New strings such as "Specimen Box List" are hardcoded English. The module has no `lang/English.ini` and doesn't use `tt()`.
