# user_story_review_migrated_boxes.md

Alice, who we discussed in `./user_story_background.md`, needs to review the boxes of historic hand-labeled specimens that Bob migrated into OST. Every migrated box and specimen starts out unverified: each box's `box_verified` and each specimen's `specimen_verified` is "No". Many of these boxes are overloaded with orphans, and their specimens have no QR codes.

## Finding migrated boxes

When Alice opens the Specimen Entry Dashboard, OST shows the box selection screen, a list of boxes. Because the CBR has _Enable verification_ turned on, the list includes the core yes/no `box_verified` field as a column. Alice filters the list to show only boxes where `box_verified` is "No", or she sorts the list by `box_verified` so the unverified boxes come first. She opens one of those boxes in the Specimen Entry Dashboard and pulls the matching physical box from the freezer. She works through the box cell by cell with the physical box in hand.

## Identifying hand-labeled specimens

Alice pulls a specimen from the physical box and reads its handwritten label. She hand-keys the participant, visit and specimen type from the label into the search field. (Matching on these specimen name components is a CURATE extension; without components, OST matches the entry against the text of specimen names.) If only one specimen matches, OST loads it into the left-hand pane and highlights its cell in the right-hand pane.

If several specimens match, OST shows a pick list of the matches. The list puts this box's orphans and unverified specimens first, then unverified specimens in other boxes, then everything else. Each row shows the match's specimen name, box, cell and verification status. Because specimens with identical labels are interchangeable, Alice picks the first suitable match. OST loads it into the left-hand pane and highlights its cell.

## Rescan Box mode with ambiguous labels

Rescan Box mode works with hand-labeled specimens too. When Alice hand-keys a label that matches more than one specimen, OST opens the same pick list instead of refusing the entry. When she chooses a match, OST proceeds as it does for a unique specimen name: it moves the chosen specimen to the selected cell, moves any displaced specimen, records the changes in the change log, advances the selected cell and marks the chosen specimen as verified.

## Orphaning specimens that aren't in the box

Alice often finds that a cell in the box grid holds a specimen that isn't in the physical box. To orphan it, she selects the cell and clicks the _Orphan_ button in the left-hand pane. OST clears the specimen's cell, leaving the specimen in the box's inventory as an orphan, and records the change in the change log. Alice can also drag the specimen from its cell onto the orphan note below the box grid. Orphaning a specimen does not change its verification status.

## Verifying specimens

Alice verifies specimens with the _Verify and Save_ button, by dragging specimens to their correct cells, or with Rescan Box mode, as described in `./user_story_verify_specimens_in_an_imported_box.md` and `./user_story_navigating_a_box_and_rearranging_specimens.md`. The _Verify entire box_ button verifies only specimens that occupy a cell. Orphans stay unverified.

## Deleting unverified orphans

When Alice has accounted for every specimen in the physical box, any orphans that remain unverified are specimens the migrated data claimed but the box doesn't hold. Alice deletes them.

- To delete one orphan, she selects it in the specimen list and clicks the _Delete_ button in the left-hand pane. The _Delete_ button is enabled only for unverified orphans. OST asks her to confirm the deletion of that specimen by name, then deletes it.
- To delete them all at once, she clicks the _Delete unverified orphans_ button below the box grid. OST asks, "Delete N unverified orphans from this box?" and deletes them when she clicks "OK".

OST never deletes a verified specimen or a specimen that occupies a cell in this way. Every deletion is recorded in the change log.

## Finishing a box

When the box has no orphans left and Alice is satisfied that the box grid matches the physical box, she clicks the _Verify entire box_ button to mark the remaining specimens and the box record as verified. OST sets the box's `box_verified` field to "Yes", so the box drops out of Alice's filtered list. She returns the box to the freezer and moves on to the next migrated box.
