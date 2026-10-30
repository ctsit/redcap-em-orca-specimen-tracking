# user_story_background.md

The user stories herein describe the management of biospecimens for a research project we'll call _CURATE_. 

## CURATE Project

The goal of CURATE is to provide phenotypic data, biospecimens, and biospecimen assay data to other studies who need it to confirm or refute their hypotheses. CURATE is a multi-site project wherein each site collects data and biospecimens to be aggregated in centralized repositories. Those data and biorepositories are managed by Enormous State University (ESU). 

The staff at the CURATE Biorepository at ESU curate biospecimens, managing the specimens, their metadata, and assay results from tests on those biospecimens. They preserve the specimens and related data for use in research studies. 

## CURATE Sites

At each CURATE site, staff collects, prepares, aliquots, labels and freezes biospecimens for temporary storage. Each aliquot has a unique ID printed on labels affixed to the tube. The labels also encode that tube ID in a QR code printed on the label. The tube IDs are often structured and include details about the research participant, collection event and tube contents. The aliquots are placed in boxes. A typical box is a 9 x 9 square with 81 cells for 81 aliquots of biospecimens from one or more research subjects. Each box has a unique name. Once loaded with a batch of specimens, the box is placed in a freezer for temporary safe-keeping.

The CURATE sites use ORCA Specimen Tracking (OST) to manage the metadata about the tubes and boxes. At a minimum, OST knows the name ID of each tube, the coordinates it occupies in the box. OST knows the name of the box, its dimensions, and if the box has been shipped. OST knows the name and date of the shipment. As OST is extensible, it can record other facts about the tube, box and shipment. CURATE uses the extensibility to record details about the tube collection and processing and extra details about shipment. These additional details provide the provenance CURATE needs to support the quality of their work and research product.

At Southern Network for Academic Clinical Care (SNACC), Dan manages the CURATE biospecimen shipments. At regular intervals, Dan ships one or more boxes of biospecimens from SNACC to the CURATE biorepository at ESU. The staff record the shipping details. They include a manifest of the contents of the boxes in the box. The manifest is a report of the data already stored in OST.

## CURATE Biorepository

The CURATE Biorepository (CBR) at ESU is managed by the Biorepository Manager, Alice. Alice is responsible for the specimens stored in the biorepository's freezers. She receives and verifies shipments from the sites, chooses locations in the freezers to store new boxes, reviews freezer and box inventory, and pulls and ships specimens for studies and assay runs.

Alice often works with Bob, the informaticist. Bob has access to the data underlying the CBR's inventory and good informatics tools. Bob runs queries of the OST site data to audit the site's biospecimen collection work. He also loads assay data coming from the labs. While Alice manages many of her queries in OST, she sometimes turns to Bob for more complex queries. 
