# user_story_site_shipment.md

Dan, who we mentioned in `./user_story_background.md`, needs to ship two boxes to the CURATE Biorepository (CBR). He opens OST, makes a new shipment record, enters the shipment's name and date, and adds two boxes to it as he loads them into an insulated shipping container. He generates a manifest in OST and prints it. Dan adds dry ice and the manifest to the shipping container, tapes it shut, prints a shipping label and affixes it to the container. He uses his barcode scanner to copy the shipment's tracking number into the OST shipment record. He re-saves the shipment record and contacts the carrier to schedule pickup.

Each time Dan saves the shipment record, OST also generates a shipment object and saves it to a file upload field of the shipment record with a name like `manifest.json`. This JSON shipment object is a permanent, coherent record of every fact in OST about the shipment and its contents.

When Dan has finished the shipment, he presses a "Send Manifest" button on the shipment record to compose an email about the shipment. The email subject and body are built from templates in OST. These templates can be overridden in the module configuration. The email sender and recipients are also configurable in the OST module configuration. When sent, the email will include two attachments. One is the current manifest CSV. The other is an export of the JSON shipment object. An OST user can import this object into their OST instance using an import feature in OST.

If Dan prefers, he can also download the shipment object in the same format the email attaches. Anyone else with access to the SNACC OST instance can do the same.
