# user_story_navigating_a_box_and_rearranging_specimens.md

## Navigation

Alice needs flexibility in how she navigates the Specimen Entry Dashboard. If her focus is in the box grid, she can use the arrow keys to move between cells. When she moves to a new cell, the left-hand pane and lower pane update asynchronously. A temporary floating label showing the specimen label also appears asynchronously near the active cell as she moves to the cell.

If Alice is in the specimen list in the lower pane, she uses the up and down arrow keys to navigate between rows. As she navigates, the other panes update asynchronously.

## Moving specimens

Inspecting a box, Alice realizes the specimens are in the wrong order. As she physically moves a specimen from one cell to another, she drags the specimen from the old cell to the new cell in the box grid. OST updates the specimen's cell as she does this. Alice can also grab a specimen from the list view and drag it to any cell in the box grid to update the specimen's cell. Each moved specimen is marked as verified. OST records each move in the change log.

If Alice drags a specimen to an occupied cell, the specimens will swap cells.

Orphaned specimens are listed at the top of the specimen list. Alice can rehome an orphan by dragging it from the list to a cell. If that cell is occupied, the specimen already there becomes an orphan, matching Rescan Box mode. Alice can also drag a specimen from a cell onto the orphan note below the box grid to orphan it.
