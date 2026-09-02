# reject-rate evaluation protocol

## purpose

this document defines how the imaging copilot program measures whether the copilot reduces rejected images in conventional radiography. it exists before the evaluation runs, so the numbers are produced by a pre-defined method and not improvised after the fact. it defines what counts as a reject, the denominator, how reject reasons are classified, who labels the images, how labeler agreement is measured, and what the comparison baseline is.

this protocol is used by the later program work, after both measurement papers (thickness and positioning) are done. it is not a claim of this study yet. this document exists so the method is ready when the copilot is.

## scope

supported projections at this stage: chest pa, pelvis ap, chest ap portable. the protocol is written per projection, because the verified literature shows reject rates and failure causes differ sharply between them.

## what counts as a reject

adopt the aapm tg-305 definition (verified, ledger v005 and v006):

- a reject is an acquisition of patient anatomy discarded by the technologist without being presented for diagnostic interpretation.
- a repeat is an additional radiograph beyond the protocol minimum that is sent to the radiologist. repeats are outside the scope of this protocol, per tg-305.
- non-patient and qc or test exposures are excluded.
- practitioner-directed repeats are excluded.

## the denominator

the rate is computed per exposure button press, per tg-305: rejected presses divided by total presses. for single-exposure acquisitions, presses equal images, which is the common case for chest pa, pelvis ap, and chest ap portable.

report the denominator convention explicitly in every result. the verified literature shows cross-study comparisons are only meaningful when the denominator is stated, because per-image deletion rates from logs differ from per-exposure-press rates.

## reject-reason classification

use the nine coarse tg-305 categories:

1. patient positioning
2. patient motion
3. image artifacts
4. image contrast or noise
5. incorrect selection (protocol, detector, body part, patient)
6. wrong body part or patient imaged
7. equipment failure
8. practitioner directed (excluded from the rate)
9. no patient exposure or test (excluded from the rate)

for the copilot's purposes, sub-classify patient positioning the way the field does:

- chest pa: rotation, inspiration depth, collimation or cone-angle cut-off (the cardiophrenic angle is the canonical failure), scapular overlap of the lung field.
- pelvis ap: rotation, tilt, superior and lateral cut-off, centring-point error.
- chest ap portable: rotation, inspiration depth, collimation, detector placement.

## primary outcome metrics

report two metrics, both per projection.

1. relative reject rate: rejected images of the projection divided by all images acquired of that projection. this is how serra (verified, v001) and lee (verified, v004) report, so results are comparable to the published benchmarks.
2. first-exposure accuracy: images accepted on the first exposure divided by all first exposures. this isolates the copilot's value, because it measures whether the first try was right. introduced by lee (verified, v004).

report both with the reject-reason breakdown mapped to the tg-305 categories.

## comparison baseline

compare the copilot condition against a baseline collected with the same method and the same denominator in the same setting. the literature does not support comparing across studies with different denominators.

benchmark references for context, all verified:

- pelvis ap relative reject rate: 17.2 percent (serra, v001), 22.5 percent in an ed audit (stephenson-smith, v002), 18.8 percent table bucky and 35.5 percent trauma trolley with first-exposure accuracy 81.8 and 56.7 percent (lee, v004).
- chest ap reject rate: 18.1 percent in an ed audit (stephenson-smith, v002).
- positioning share of rejects: 76 percent (serra, v001), 79.4 and 77.3 percent (bantas, v007), 66.67 percent positioning or breathing for chest (songklanakarin, v008).

## labelling ground truth

reject reason codes are assigned by the technologist at rejection time, but the verified literature shows reason codes are subjective and often wrong. therefore:

- every rejection in the evaluation sample is reviewed by an expert radiographer against the image, not taken from the coded reason alone.
- labeler agreement is measured with cohen's kappa for categorical reasons and intraclass correlation for continuous measurements. the arlex-p study (in sweep notes, not ledger-verified) reported pelvis centring inter-observer icc as low as 0.24, which means ground truth must be built and its reliability quantified, not assumed.
- the evaluation reports the agreement numbers alongside the reject rates.

## exposure index as a confounding check

exposure index and deviation index are used as a check that exposure practice did not drift while positioning improved, not as the primary outcome. the verified literature (sweep section 5) shows ei/di are validation and qc tools, not reject predictors, and that ei is blind to positioning corruption of the segmentation region of interest.

## ethics

the eventual evaluation against real recorded patient positioning requires ethics approval before any data collection. this protocol is method-only and does not authorize collection. no human-subject data is collected under this document.

## reproducibility

every evaluation run records: the date range, the room, the projection, the denominator, the labeler identities and their agreement, the model version of any copilot software involved, and the exact commands that produced the numbers.

## status

draft. not yet used. pending the two measurement papers and the working copilot.