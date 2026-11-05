# current_state_comparison.md

This document compares the user stories with OST as it exists on this branch. File references are relative to the module root and were accurate on 2026-11-05.

**Today:** _Exists_ means OST already does what the story describes. _Partial_ means some of it exists. _New_ means OST has nothing like it. **Scope:** _Core_ is OST behavior. _CURATE_ is a CURATE extension (see "OST core fields and CURATE extensions" in `./user_story_background.md`).

## Summary

Today OST supports:

- scan-driven entry of new specimens into boxes;
- moving one specimen at a time to the next free cell;
- site-side shipping: a CSV manifest and a _Complete Shipment_ action.

The stories add four things:

1. **Receiving:** a JSON shipment object, a _Send Manifest_ email, and import at another OST instance.
2. **Verification:** a verified state for specimens, boxes and shipments.
3. **In-place work in the Specimen Entry Dashboard:** selecting, browsing, editing and rearranging specimens.
4. **Cleanup of legacy data**, supported by a persistent **change log**.

Several of these change existing behavior. They are listed under "Changes to existing behavior" below.

## Site shipment

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Create shipment, add and remove boxes | Exists | Core | `traits/ShipmentUtils.php:386-438`, `src/components/ShipmentMain.vue:193-230` | |
| Shipment date, tracking number | New | CURATE | No such fields in code | Local fields |
| Printable manifest | Partial | Core | `manifest-export.php` | CSV only. Columns are chosen per field with the "shipment-manifest" flag. |
| JSON shipment object saved on each save | New | Core | — | Needs new `shipment_object` field |
| _Send Manifest_ email with templates, sender and recipients | New | Core | — | No `REDCap::email` call. Settings would go in `state.general`. |
| Download the shipment object | New | Core | — | Only the CSV can be downloaded today |

## Verify specimens in an imported box

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Import the shipment object, with a uniqueness check | New | Core | — | Specimen-name uniqueness is enforced only in the browser, where a scan of an existing name becomes a move (`SpecimenForm.vue:357-375`). Import needs a server-side check. |
| Verified and unverified state | New | Core | — | Needs `box_verified`, `specimen_verified`, `shipment_verified`. Box status today is only available or closed. |
| Find a box by scanning a specimen | Partial | Core | `traits/PlateUtils.php:145-229`, `BoxListModal.vue` | Search returns boxes, not specimens, and doesn't highlight the match |
| Grid, details and list panes | Partial | Core | `DashboardMain.vue:674-812` | The panes exist. The top-left form is for new specimens only. |
| _Verify and Save_, _Verify entire box_ | New | Core | — | |
| Rescan Box mode | Partial | Core | `SpecimenForm.vue:33-49, 844-881` | A single "Moving" dialog sends the specimen to the next empty cell. There is no mode, no swap and no log. |
| Unknown specimen goes to new-specimen entry | Partial | Core | `traits/SpecimenUtils.php:143-241` | A scan with no match already starts new entry, including parsing name parts |
| Orphans | New | Core | `DashboardMain.vue:375-389` | Today a missing position is a **critical error** that makes the dashboard read-only |

## Browse specimens

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Click a cell or list row to load the specimen | New | Core | `DashboardMain.vue:356-360, 404-412` | Only empty cells react to clicks. Occupied cells just show a hover tooltip. |
| Grid, details and list stay in sync | Partial | Core | `DashboardMain.vue:320-355` | Panes update only after a save |
| Provenance fields in the details | Exists | CURATE | | Any added field can appear in the form |

## Navigating a box and rearranging specimens

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Arrow keys in the grid and list | New | Core | — | Enter moves between form fields (`SpecimenForm.vue:530-546`) |
| Floating label on the active cell | Partial | Core | `DashboardMain.vue:404-412` | Native hover tooltip only |
| Drag and drop, swap, rehome orphans | New | Core | — | |

## Edit specimens

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Edit in the left-hand pane | Partial | Core | `DashboardMain.vue:292-297`, `SpecimenModal.vue` | Edits happen in a separate modal opened from the list |
| Save that leaves verification unchanged | New | Core | — | Depends on verification |

## Review migrated boxes

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Box selection screen on open | Exists | Core | `DashboardMain.vue:495-532` | Lists **Available** boxes only (`PlateUtils.php:179-184`) |
| `box_verified` column | Partial | Core | `src/components/BoxList.vue:45-53` | Columns can be configured since `c1f2a72`, but they show raw codes (`1`/`0`), not labels |
| Sort and filter the box list | New | Core | `BoxList.vue` | No `sortable` and no filters. `ShipmentSearch.vue` already uses PrimeVue's global filter. |
| Match on name components, with a pick list | Partial | CURATE | `SpecimenUtils.php:212-223` | Search returns one record: an exact match or the first partial match |
| _Orphan_ button, drag to orphan | New | Core | — | |
| _Delete_ one specimen | Exists | Core | `SpecimenUtils.php:286-306`, `DashboardMain.vue:842-870` | Already confirmed with a dialog. Not limited to orphans. |
| _Delete unverified orphans_ | New | Core | — | No bulk delete today |

## Change log

| Feature | Today | Scope | Evidence | Note |
|---|---|---|---|---|
| Log every data change to the EM log | Partial | Core | `traits/ShipmentUtils.php:208-432`, `traits/HookUtils.php:35, 93` | `$module->log()` records errors only. Saves and deletes are not logged. |
| Change log pane | New | Core | — | Nothing in the UI reads the log. N would be a new `state.general` setting. |

## Changes to existing behavior

These items change how OST works today, so they need the OST authors' agreement more than anything else:

1. **Four new required fields:** `box_verified`, `specimen_verified`, `shipment_verified`, `shipment_object`.
   - Existing installations must add them on upgrade, and the module README's "Project Requirements" section must list them.
   - _Enable verification_ hides the verification UI for sites that only do data entry.
2. **Orphans become a normal state.** Today a missing position is a critical error that makes the dashboard read-only.
3. **The entry form becomes the left-hand pane** for viewing and editing any specimen. It replaces both the new-specimen-only form and the Edit modal.
4. **Selection works everywhere.** Clicking an occupied cell or a list row selects that specimen.
5. **The box list shows choice labels and supports sorting and filtering.** Which boxes it lists (Available only) may also need to change.
6. **Specimen-name uniqueness is enforced on the server**, for import.
7. **Logging records every data change**, not just errors.
8. **New general settings** (_Enable verification_, change log N, email templates) must be added to the whitelist in `traits/ConfigUtils.php:272-277`. Otherwise they are saved but never read back.

## Defects noticed while comparing

I confirmed each of these by reading the code. None of them is covered by the stories.

- `src/components/SpecimenForm.vue:370` calls `this.$nextTick` inside `<script setup>`, where `this` is undefined. The "exists on a closed box" error path will throw.
- `src/components/DashboardMain.vue:118`: the `sortedSpecimens` computed calls `.sort()` on `specimens.value`, which reorders the source array in place.
- `src/components/DashboardMain.vue:384` indexes `positions.value[row][col]` without checking bounds. A position outside the box size will throw.
- `traits/ShipmentUtils.php:188` indexes the result of `getShipment()` by `firstEventId` a second time. `getShipment()` already returns the event-level array (`:42`), so the "status is already …" check never fires.
- `manifest-export.php:31` calls `reset($data)` on the result of `getShipmentManifestData()`. That result is empty for a shipment with no boxes (`ShipmentUtils.php:101-107`), so the export fails instead of showing an error.
