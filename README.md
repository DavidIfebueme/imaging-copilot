# imaging copilot

a real-time copilot for conventional x-ray imaging. a plain webcam watches the patient. before the exposure, the copilot checks patient centering, rotation, and symmetry, and suggests exposure factors from camera-measured body thickness. it advises only. it never touches or controls the x-ray machine.

## why this exists

positioning errors are the top cause of rejected images in digital radiography: 76 percent in a multi-centre study (serra 2024, j med radiat sci 10.1002/jmrs.796), 77 to 79 percent across two departments in another (bantas 2023, 10.1002/jmrs.654). camera-based centering is solved for ct. for radiography, no published system gives pre-exposure positioning feedback from an ordinary rgb webcam. this project works in that gap.

## how it works

two tracks run side by side on one webcam feed.

the positioning track finds landmarks and measures rotation and symmetry against the centering points and tolerances of the current department.

the exposure track estimates body thickness in centimeters with monocular depth (depth anything v2 small, apache-2.0), anchors the depth scale to the known detector plane, then maps thickness through the department technique profile, interpolating between the department's own calibration points.

departments differ on centering points, tolerances, and technique steps. the operator changes these by talking to an ai agent. the agent edits a versioned technique profile (json) whose shape is governed by a schema. deterministic code reads that file at runtime and produces every recommendation. the llm never computes live advice.

## constraints

the stack is open source and runs on consumer hardware.

data comes from public datasets (chexpert, mimic-cxr) and synthetic scenes built from smpl-x bodies in simulated rooms. physical validation follows the same geometry: a calibrated plane, known reference distances, controlled lighting.

scope covers three projections first: chest pa (wall bucky), pelvis ap (table bucky), and chest ap portable (bedside). other views come only after these are solid.

research discipline applies from day one: every claim the project relies on lives in the verification ledger with its primary source and quote. score recorded sessions before any live use, and get ethics approval before collecting any human-subject data.
