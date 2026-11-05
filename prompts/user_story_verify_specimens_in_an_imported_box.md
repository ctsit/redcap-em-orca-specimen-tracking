# user_story_verify_specimens_in_an_imported_box.md

## Receipt of a shipment

Alice, who we discussed in `./user_story_background.md`, manages the CURATE Biorepository (CBR). Among her many tasks, she receives and verifies shipments from the CURATE sites. When she receives a shipment, she checks her email for a message from Dan and the SNACC OST system about the shipment. If she doesn't have one, she requests it from Dan or the local CURATE admins who have access to the SNACC OST system. With the shipment object (`manifest.json`) in hand, Alice opens the CBR OST as she unboxes the shipment. She opens the received shipment interface and imports the shipment object. OST verifies that the box names and specimen names are unique. If anything has a duplicate in the CBR, OST generates a detailed, exportable warning about non-unique items and refuses to load the shipment. If everything is unique, OST loads the new items and marks every box and specimen in the shipment as unverified. OST records the import in the change log.

## Verification of a shipment

Alice now needs to verify that the shipment reflects the data in the imported shipment object. Alice removes the first box of specimens from the shipping container. She checks the box for a name.

- If she finds a name, she locates that box in the imported shipment and opens it.
- If Alice doesn't see a name on the box, she pulls a specimen from the box and scans it into a search field. OST presents any records that match and offers a button to open any of the matches. For a QR-coded specimen, there should be only one match. Alice opens the match.

With either course, OST opens the Specimen Entry Dashboard to that box. This presents a graphical representation of the box on the right, details about the selected specimen on the left, the change log in a full-width pane beneath them, and a list of the box's specimens below that.

Alice can verify the box visually or with the hand-held scanner. For visual verification, Alice pulls a specimen from the physical box to read its specimen name. She visually confirms the name on the tube matches the specimen name of the same cell in the box. She can verify the specimen name in the list view, or she can click on the cell in the box to load its values into the specimen details in the left-hand pane.

To verify a specimen with the scanner, Alice can pull the specimen and scan its QR code into a search field in the Specimen Entry Dashboard. In response to this search, OST will highlight the specimen's expected cell in the right-hand pane and load its values in the left-hand pane.

### Acknowledging specimens that match the imported shipment

Any time Alice loads a specimen record she's happy with, Alice can click the _Verify and Save_ button in the left-hand pane. The left-hand pane also has a plain _Save_ button that saves edits without changing the specimen's verification status.

Alice repeats these operations for several specimens until she is satisfied the shipment data is accurate. She can verify as many or as few as she likes. When she is satisfied the box is accurate, Alice clicks the _Verify entire box_ button. In response, a dialog opens and asks, "Do you want to mark every specimen in a cell and the box record as verified?" Alice clicks "OK", ignoring the "Cancel" button. Orphans are not verified.

### Fixing mismatch between specimen location and the imported shipment

If Alice finds a specimen in the wrong box cell, she needs to match the specimen location to the shipment data or vice versa. OST has a _Rescan Box_ feature to help her re-inventory all or part of a box. Rescan Box mode is designed for moving known specimens between cells and boxes. Aside from the box and cell, Rescan Box mode does not allow editing of a specimen. In Rescan Box mode, OST disables editing in the left-hand pane, exposes a specimen name search field, and positions the cursor in the search field. Data entry in the search field will auto-complete any specimen name. With a unique specimen name of an existing specimen in the search field, pressing the Enter key will (for hand-labeled specimens whose labels match several records, see `./user_story_review_migrated_boxes.md`):

1. Move the scanned specimen to the selected cell on the box grid, setting the box ID as well if needed.
2. Move the displaced specimen (if any) to the box and cell previously allocated to the scanned specimen.
3. Record the changes in the change log (see `./user_story_change_log.md`).
4. Advance the selected cell to the next cell in the box moving left-to-right then top-to-bottom.
5. Mark the scanned specimen as verified.

If the scanned specimen came from another box, the displaced specimen moves to that box. If the scanned specimen was an orphan, the displaced specimen becomes an orphan in the scanned specimen's former box.

Alice continues scanning specimens, pulling the specimen from the next-selected cell, scanning it and returning it to that cell until she has rescanned and rehomed every specimen that needed verification. When she has finished, Alice clicks the _Exit Rescan Box_ button to leave Rescan Box mode.

Note that the search field works equally well with hand-keyed and scanned specimen names. The scanning method is quite efficient as every scan is terminated with an Enter keystroke. This allows cells to be checked as fast as the QR codes can be scanned.

### Managing unknown specimens in Rescan Box mode

In Rescan Box mode, OST will not allow editing of existing specimens or data entry of new specimens—it only moves them between cells and boxes. If a specimen name entered in Rescan Box mode is not in OST's inventory, OST will offer to exit Rescan Box mode to do new data entry. If Alice agrees, OST moves any specimen assigned to that cell to an orphaned position in the same box. The specimen will stay in the box's inventory, but will have a null value in the cell field. The specimen stays with the box but is otherwise homeless until it is rehomed. OST records this change in the change log.

OST then copies the value from the search field into the specimen name field. When she presses Enter, OST parses the specimen name to extract any components from a structured name and proceeds with normal OST data entry mode for new specimens. When Alice saves the new specimen, OST returns to Rescan Box mode and advances the selected cell to the next cell in the box.

### Managing orphaned specimens

If a box has one or more orphaned specimens, the right-hand pane will include a note to this effect just below the box. Orphans will be listed at the top of the specimen listing in the lower pane regardless of sort order.
