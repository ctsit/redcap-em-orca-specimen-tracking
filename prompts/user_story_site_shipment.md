# user_story_site_shipment.md

Dan, who we mentioned in `./user_story_background.md`, needs to ship two boxes to the CURATE Biorepostory (CBR). He opens OST, makes a new shipment record, and adds two boxes to it as he loads them in an insulated box for shipment. He generates a manifest in OST and prints it. Dan adds dry ice and the manifest to the box, tapes the box shut, prints a shipping label and affixes it to the box. He uses his barcode scanner to copy the shipment's tracking number into the the OST shipment record. He re-saves the shipment record and contacts the shipper for the pickup. 

Each time Dan saves the shipment record, OST also generates a shipment data object and saves it to a field on the shipment record. This JSON object is permanent, coherent record of every fact in OST about the shipment and its contents. 

When Dan has finished the shipment, he presses a "Send Manifest" button on the shipment record to compose an email about the shipment. The email subject and body are built from templates in OST. These templates can be overridden in the module configuration. The email sender and recipents are also configurable in the OST module configuration. When sent the email will include two attachments. One is the current manifest CSV. The other is an export of the JSON shipment object as a file attachment. An OST user can import this object into their OST instance using an import feature in OST.

If Dan prefers, he can also download the shipment object in the same format that email sends. Anyone else with access to the SNACC OST instance can do the same. 
