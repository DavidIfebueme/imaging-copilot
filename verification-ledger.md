# verification ledger

every claim this project relies on gets an entry here before we build on it. a claim is verified only when someone read the primary source (the paper, the standard, the official docs) and recorded the exact quote and where it came from. agent-written summaries of abstracts do not count as verified.

columns: id, claim, source, pmid/doi, quote, verified on, verified by.

verified:

| id | claim | source | pmid/doi | quote | verified on | verified by |
|----|-------|--------|----------|-------|-------------|-------------|
| v001 | positioning is the top reject cause in digital radiography at 76% | serra et al. 2024, journal of medical radiation sciences | pmid 38845126, doi 10.1002/jmrs.796 | "the most frequent reasons for image rejection were patient positioning (76%) and patient motion (7.5%)." | 2026-08-31 | agent read full pubmed abstract |
| v002 | ap chest and ap pelvis have high relative reject rates in an ed room | stephenson-smith et al. 2021, journal of medical radiation sciences | pmid 33826800, doi 10.1002/jmrs.468 | "the projections with both a high number and high percentage of rejects were antero-posterior (ap) chest (175, 18.1%), ap pelvis (78, 22.5%), horizontal beam hip (61, 33.5%) and horizontal beam knee (116, 30.5%)." | 2026-08-31 | agent read full pubmed abstract |
| v003 | positioning dominates multiple-reject reasons | stephenson-smith et al. 2021 | pmid 33826800, doi 10.1002/jmrs.468 | "the top reasons for multiple rejects were positioning (67.1%) and anatomy cut-off (8.4%)." | 2026-08-31 | agent read full pubmed abstract |
| v004 | pelvis on trauma trolley rejects far more than on table bucky, and first-exposure accuracy is much lower | lee et al. 2025, journal of medical radiation sciences | pmid 40583231, doi 10.1002/jmrs.70004 | "the mean reject rate and the first exposure accuracy of pelvis x-rays taken on a trauma trolley were 35.5% and 56.7% respectively, while the mean reject rate and the first exposure accuracy for images taken on a table bucky were 18.8% and 81.8%, respectively (p < 0.01). the superior and lateral anatomy cut-off were the major causes of image rejection for both techniques." | 2026-08-31 | agent read full pubmed abstract |
| v005 | reject analysis lacks vendor-neutral standards, which aapm moved to fix | aapm task group report 305, little et al. 2023, journal of applied clinical medical physics | pmid 36995917, doi 10.1002/acm2.13938 | "due to the lack of standardization, reject data often cannot be easily compared between radiography systems from different vendors." | 2026-08-31 | agent read full pubmed abstract |
| v006 | tg-305 proposes a schema for classifying reject reasons and reporting workflows | aapm tg-305, little et al. 2023 | pmid 36995917, doi 10.1002/acm2.13938 | "essential data elements, a proposed schema for classifying reject reasons, and workflow implementation options are recommended in this task group report." | 2026-08-31 | agent read full pubmed abstract |

pending verification (claimed in agent sweep notes, not yet read from the primary source):

| id | claim | source to check | note |
|----|-------|-----------------|------|
| p001 | chest pa deletes at ~5% vs ap chest 18% | oudiz et al. 2021 (per sweep notes) | sweep attributed this to jmrs.468 which is stephenson-smith, not oudiz. the attribution is suspect. verify before use. |
| p002 | inspiration/breathing is 66.7% of chest rejects in one audit | songklanakarin audit per sweep notes | exact paper unknown. find and verify. |
| p003 | overall dr reject rates cluster 9-11% | serra 2024, oudiz 2021, lrrl | serra abstract verified but the 9-11% cluster claim is my aggregation, not a quote. re-derive from verified sources. |
| p004 | ai reject automation exists post-exposure only (auc 0.97 chest) | dunnmon radiology 2018; liu medrxiv 2024 / jmrs 2025 | not read. verify. |
| p005 | depth anything v2 small is apache-2.0; base/large are cc-by-nc | huggingface model card | not read. verify against the model card. |
| p006 | bucky-anchored monocular depth plausible at +/-1-2 cm thickness | synthesis of sweep 02, no single source | this is an engineering judgment, not a paper finding. it needs experimental validation, not a citation. |
| p007 | mimic-cxr requires credentialing; chexpert has its own license terms | mimic-cxr and chexpert official pages | not read. verify before using either dataset. |
| p008 | glm-5.3-flash multimodal with 1m window | opencode go docs | not read from docs directly. verified only by api test that image input returns a valid response. confirm docs. |

how to add an entry:

- find the primary source (paper, standard, model card, official docs).
- read the part that supports the claim, not a summary of it.
- copy the exact supporting sentence into the quote column.
- record pmid/doi or url, the date, and who verified (you, the agent name).
- never copy a claim from the pending section into a build artifact or a doc as if it were verified.

how to resolve a pending entry:

- move it to the verified table when the quote is confirmed.
- change the note to explain what was found, or drop the claim if the source does not support it.