# paper 1: thickness measurement from an anchored webcam

## working title

accuracy of bucky-plane-anchored monocular depth for estimating body thickness in radiography

## research aim

this is the first paper in the imaging copilot program. it establishes whether a single ordinary webcam can measure patient thickness in centimeters well enough to support exposure factor selection in conventional radiography. the eventual program aim, a radiographer using the copilot to reduce repeat exposures, depends on this measurement being correct, so this paper comes first and publishes on its own.

## research question (one primary)

what is the accuracy of webcam monocular depth, anchored to a known reference plane, for estimating object thickness at clinical distances?

## hypothesis

a webcam running a monocular depth model, with its depth scale anchored to a known flat reference plane, estimates the thickness of an object placed against that plane with a mean absolute error under 2 cm at working distances of one to three meters, across the measured thickness range.

## why this question matters

exposure factors (kvp and mas) in radiography are chosen from the patient's thickness. currently the radiographer estimates that thickness by eye, which is subjective. a camera-measured number replaces the guess with a measurement. no published system does this from an ordinary rgb webcam (negative claim from the sweeps, still pending in the ledger).

## method outline

- hardware: one consumer webcam at known position, one flat reference plane standing in for the wall bucky detector.
- objects: solid blocks of known thickness spanning the clinically relevant range for chest and pelvis, roughly 15 to 35 cm, to be confirmed against published technique data before the method is final.
- depth models: depth anything v2 small (verified apache-2.0, ledger v010) as the baseline. a native metric model in the md2e class as the comparison arm, because md2e outputs absolute depth without our anchoring trick (model claims unverified, marked pending).
- anchoring: convert the model's relative depth to centimeters using the known reference plane, per the design in the repo readme.
- ground truth: measured thickness of each block with a calibrated reference, not the model's own output.
- outcome: mean absolute error, root mean square error, and bias between predicted and true thickness, reported per distance and per thickness.
- reproducibility: every command, model version, and parameter recorded next to the results.

## ethics position

no human subjects. the objects are solid blocks. no ethics approval required. the ethics statement in the paper will say exactly this, that measurement validation used inanimate objects only.

## evaluation protocol reference

this paper reports measurement accuracy only. it does not yet report reject-rate reduction. the reject-rate evaluation protocol is a separate document used by the later program work, because this study cannot claim clinical outcome before the measurement is proven.

## what success looks like

mean absolute error under 2 cm across the measured range at clinical distances, with the error stated per thickness band. if the metric model beats anchored depth, the pipeline simplifies and the anchoring design is revised. if neither reaches 2 cm, the exposure track needs a different sensing approach and the paper reports the negative result honestly.

## trajectory

this paper feeds the program aim by proving exposure measurement. paper 2 (positioning accuracy) does not depend on its results, only on the shared geometry and camera assumptions. publishable alone as a methods and validation study.

## open questions before drafting

- which exact metric model to include as the comparison arm, pending ledger verification of license and claims.
- whether the depth runtime is webgpu in browser or local python, pending verification of the real-time performance claim.
- the precise block thickness set and number of repetitions, to be fixed in the method section.