# user_story_change_log.md

Every change OST makes to a box or specimen is recorded in OST's change log. The change log supplements REDCap's own logging: REDCap records that a record changed, and the change log records which OST action changed it and why. OST writes the change log to the REDCap external module log for the OST module, so it persists across sessions and is shared by everyone who uses the project.

## What is recorded

Each entry records:

- when the change happened and which user made it
- the box and specimen affected
- what changed, with old and new values (for example, cell B4 → C7, or unverified → verified)
- the OST action that caused it, such as shipment import, Rescan Box mode, drag and drop, _Orphan_, _Delete_, _Delete unverified orphans_, _Save_, _Verify and Save_ or _Verify entire box_

A single action that changes several records, such as a swap or _Verify entire box_, writes one entry per record changed. The entries are linked so they read as one action.

## The change log pane

The Specimen Entry Dashboard shows the change log in a full-width pane between the left-hand and right-hand panes above it and the specimen list in the lower pane below it. It sits there so Alice can see each change as she works. A glance at the change log after she moves or edits a specimen confirms the change was the one she intended, or alerts her to one she didn't intend. The pane shows the most recent N entries for the box that is open, oldest at the top and newest at the bottom, and scrolls to the newest entry as each change is made. OST briefly highlights each new entry. N is set in the module configuration.

Because the change log is persistent, the pane shows earlier work when Alice reopens a box. That includes changes she made yesterday and changes made by other users. If Alice is interrupted in the middle of reviewing a box, the pane shows her where she left off.

Only changes made through OST appear in the change log. Changes made outside OST, such as Bob's migration of the historic hand-labeled specimens, are recorded only in REDCap's own logging. A freshly migrated box therefore has an empty change log until Alice starts reviewing it.

The change log is read-only. Alice cannot edit or delete entries, and the pane does not undo changes.

## Using the full change log

Bob can review the complete change log, for every box, with REDCap's external module log view or his own queries. He uses it to audit how a box reached its current state, for example to see which orphans Alice deleted and when.
