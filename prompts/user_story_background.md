# user_story_background.md

The user stories herein describe the management of biospecimens for a research project we'll call _CURATE_.

## CURATE Project

The goal of CURATE is to provide phenotypic data, biospecimens, and biospecimen assay data to other studies who need it to confirm or refute their hypotheses. CURATE is a multi-site project wherein each site collects data and biospecimens to be aggregated in centralized repositories. Those data and biorepositories are managed by Enormous State University (ESU).

The staff at the CURATE Biorepository at ESU curate biospecimens, managing the specimens, their metadata, and assay results from tests on those biospecimens. They preserve the specimens and related data for use in research studies.

## CURATE Sites

At each CURATE site, staff collects, prepares, aliquots, labels and freezes biospecimens for temporary storage. Each specimen is an aliquot in a labeled tube. Each specimen has a unique specimen name printed on a label affixed to the tube. The label also encodes that specimen name in a QR code. The specimen names are often structured and include details about the research participant, collection event and specimen contents. The specimens are placed in boxes. A typical box is a 9 × 9 grid with 81 cells for 81 specimens from one or more research participants. Each box has a unique name. Once loaded with a batch of specimens, the box is placed in a freezer for temporary safekeeping.

The CURATE sites use ORCA Specimen Tracking (OST) to manage the metadata about the specimens and boxes. At a minimum, OST knows the name of each specimen and the coordinates it occupies in the box. OST knows the name of the box, its dimensions, and whether the box has been shipped. OST knows the name and date of the shipment. As OST is extensible, it can record other facts about the specimen, box and shipment. CURATE uses the extensibility to record details about the specimen collection and processing and extra details about shipment. These additional details provide the provenance CURATE needs to support the quality of their work and research product.

At Southern Network for Academic Clinical Care (SNACC), Dan manages the CURATE biospecimen shipments. At regular intervals, Dan ships one or more boxes of biospecimens from SNACC to the CURATE Biorepository at ESU. Dan records the shipping details. He includes a manifest of the contents of the boxes in the shipping container. The manifest is a report of the data already stored in OST.

## CURATE Biorepository

The CURATE Biorepository (CBR) at ESU is managed by the Biorepository Manager, Alice. Alice is responsible for the specimens stored in the biorepository's freezers. She receives and verifies shipments from the sites, chooses locations in the freezers to store new boxes, reviews freezer and box inventory, and pulls and ships specimens for studies and assay runs.

Alice often works with Bob, the informaticist. Bob has access to the data underlying the CBR's inventory and good informatics tools. Bob runs queries of the OST site data to audit the sites' biospecimen collection work. He also loads assay data coming from the labs. While Alice runs many of her queries in OST, she sometimes turns to Bob for more complex queries.
