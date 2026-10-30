# user_story_verify_tubes_in_an_imported_box.md

!!! Update these sections to reflect the export/import manifest workflow!!!
Bob, who we discussed in `./user_story_background.md`, wrote a script, `copy_site_shipment_to_biorepo`, that checks for new shipping records nightly. Bob's script detects the new shipping record and queries the site OST data to get all the details for the shipment and every box and specimen in it. Then the script copies those details to new box and specimen records in the CURATE BioRepository (CBR) and marks the boxes and tubes as unverified. The script creates a new shipment receipt record with every detail of the boxes and specimens in a JSON object. It marks the shipment receipt record as unverified as well.

Alice, who we discussed in `./user_story_background.md`, receives and verifies shipments from the CURATE sites. Bob's script tells her the new shipment is on its way and that she'll need to verify the shipment box and box contents when the shipment arrives. When the shipment arrives, Alice opens the CBR OST as she unboxes the shipment. She opens the received shipment interface where she sees only the new unverified shipment. All of the verified shipment are hidden by default. She can expose them with one click, but by default they are hidden.

When a CURATE site makes a shipment,
