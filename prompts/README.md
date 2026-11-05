# OST user stories: reader's guide

OST was built for scan-driven entry of new specimens into boxes and for shipping those boxes from a site. These user stories propose four additions:

1. **Receiving:** a JSON shipment object, a _Send Manifest_ email, and import at the receiving OST instance.
2. **Verification:** a verified state for specimens, boxes and shipments, so imported and migrated data can be checked against the physical specimens.
3. **In-place work in the Specimen Entry Dashboard:** browsing, editing and rearranging specimens.
4. **Cleanup of legacy data:** support for migrated data, backed by a persistent change log.

To support verification and receiving, the stories propose four new required fields: `box_verified`, `specimen_verified`, `shipment_verified` and `shipment_object`. Sites that only do data entry can hide the verification features.

The stories describe what users need to do, not how OST should implement it. They also separate OST core behavior from CURATE's local extensions. Some of the proposals change how OST behaves today. [The current-state comparison](./current_state_comparison.md) lists what already exists and what would change. We'd like your feedback before we design or write any code.

## Reading order

The stories follow a specimen from a collection site to the biorepository: it is shipped, received and verified, then browsed, rearranged and edited. Next comes the cleanup of legacy data, which combines the earlier features and adds a few more. The change log comes last because every other story refers to it.

| # | Story | Read time | Stage | Today | Features to review |
|---|-------|-----------|-------|-------|--------------------|
| 1 | [Background](./user_story_background.md) | ~4 min | Context | — | None. Introduces CURATE, its people, and the historic hand-labeled specimens |
| 2 | [Site shipment](./user_story_site_shipment.md) | ~1 min | Ship | Partial | Shipment object saved as `manifest.json`; _Send Manifest_ email with configurable templates, sender and recipients; manifest CSV and shipment object attachments; shipment object download |
| 3 | [Verify specimens in an imported box](./user_story_verify_specimens_in_an_imported_box.md) | ~5 min | Receive and verify | Mostly new | Shipment import with uniqueness check; unverified status; _Verify and Save_, _Save_, _Verify entire box_; Rescan Box mode; unknown specimens; orphans |
| 4 | [Browse specimens](./user_story_browse_specimens.md) | ~1 min | Review | Changes existing | Box grid, left-hand pane and specimen list stay in sync |
| 5 | [Navigating a box and rearranging specimens](./user_story_navigating_a_box_and_rearranging_specimens.md) | ~1 min | Review and rearrange | New | Arrow-key navigation; floating label; drag and drop with swaps; rehoming orphans; moves mark specimens verified |
| 6 | [Edit specimens](./user_story_edit_specimens.md) | <1 min | Edit | Changes existing | Plain _Save_ leaves verification status unchanged |
| 7 | [Review migrated boxes](./user_story_review_migrated_boxes.md) | ~3 min | Clean up legacy data | Mostly new | `box_verified` filter and sort on the box selection screen; pick list for ambiguous labels; _Orphan_; _Delete_ and _Delete unverified orphans_ |
| 8 | [Change log](./user_story_change_log.md) | ~2 min | Cross-cutting | New | Persistent change log in the EM log; change log pane; auditing |
| 9 | [Current-state comparison](./current_state_comparison.md) | ~6 min | Reference | — | What exists today, what changes, and defects noticed |

**Short on time?** Read 1, 3, 7 and 8, and then the "Changes to existing behavior" section of the comparison (9). Together they cover most of the new behavior.

## Vocabulary

- **Specimen**: one aliquot in a labeled tube, identified by its unique **specimen name**.
- **Box**, **cell**: a specimen box and one position in its grid.
- **Orphan**: a specimen that belongs to a box but has no cell.
- **Verified / unverified**: whether a specimen or box record has been confirmed against the physical item. It is stored in the proposed required yes/no fields `specimen_verified` and `box_verified`. A shipment's `shipment_verified` becomes "Yes" when all of its boxes are verified. The _Enable verification_ setting shows or hides the verification UI.
- **`shipment_object`**: the proposed required file upload field on the shipment record. It holds the shipment object.
- **Core / CURATE extension**: core fields and behavior are required in every OST installation. CURATE extensions, such as the shipment date, the tracking number, provenance fields and specimen name components, are local to CURATE.
- **Specimen Entry Dashboard** panes:
  - **left-hand pane**: details of the selected specimen
  - **right-hand pane**: the box grid
  - **change log pane**: full width, below the left-hand and right-hand panes
  - **lower pane**: the specimen list
- **Rescan Box mode**: a mode for moving known specimens between cells by scanning them.
- **Manifest**: the human-readable CSV or printout of a shipment.
- **Shipment object**: the complete JSON record of a shipment.
- **Change log**: OST's persistent record of the changes it makes.

## What feedback we want

For each feature, please tell us:

- Does it fit OST's design?
- Does it conflict with work you have planned?
- Would you approach it differently?

Please also tell us if a feature already exists or seems out of scope.

## Not a story

[`redcap-em-review-findings.md`](./redcap-em-review-findings.md) is a code-review report on this branch, not a user story. You can skip it while reviewing the stories.

[`base_projects/`](./base_projects/) contains REDCap XML templates of the three OST base projects. They define today's core fields, without the four proposed fields.
