# Project specification
# Beam Designer

## Purpose
Beam Designer is for engineering students and users performing preliminary
beam evaluations. Given a simply supported beam or cantilever, its span,
point or uniform loads, and a steel W-shape or lumber size, the app calculates
support reactions and presents shear, moment, and deflection diagrams. It
compares bending stress with the allowable stress and deflection with the
selected deflection limit, which defaults to L/360, to help users understand
the beam's response and assess whether it satisfies these checks.

Expected units: span in feet (ft); point loads, reactions, and shear in kips
(kip); uniform loads in kips per foot (kip/ft); moment in kip-feet (kip-ft);
deflection in inches (in); and bending stress in kips per square inch (ksi).

## Inputs
- **Beam:** Select simply supported or cantilever. Enter a span greater than
  zero in feet (ft).
- **Member:**

  | Member type | Selection method | Example |
  | --- | --- | --- |
  | Steel W-shape | Choose a designation from a dropdown of available shapes. | W12x26 |
  | Lumber | Provide the size, species, and grade. | — |

  The selected member must have defined section properties and material
  values for the bending and deflection checks.
- **Point loads:** Enter each load's magnitude in kips (kip), its location in
  feet (ft) measured from the left end or the cantilever's fixed end, and its
  direction.
- **Uniform loads:** Enter each load's intensity in kips per foot (kip/ft),
  its start and end locations in feet (ft), and its direction. Both locations
  must be within the span, and the end location must be after the start.
- **Load entry control:** In each load case, provide a dropdown to select
  either a point load or a uniformly distributed load (UDL), followed by an
  Add load action.
- **Load cases:** Allow users to define multiple load cases and assign each
  point or uniform load to a case. Analyze each case separately.
- **Deflection limit:** Allow users to configure the span-to-deflection ratio,
  defaulting to L/360. Apply the selected ratio to both simply supported beams
  and cantilevers.
- **Units and validation:** Use the units listed in Purpose and show them next
  to the input fields. Reject missing values, nonpositive spans, and load
  locations outside the beam.

## Calculations
- For each load case, solve static equilibrium for the support reactions.
- Calculate shear and moment along the beam, accounting for point loads and
  the start and end of uniform loads. Use a documented sign convention and
  identify the maximum absolute shear and moment.
- Calculate the deflection curve using the selected member's modulus of
  elasticity (E), moment of inertia (I), and the beam's support conditions.
  Identify the maximum absolute deflection and its location.
- Calculate maximum bending stress as `fb = |Mmax| / S`, using the member's
  section modulus (S), and compare it with the allowable bending stress (Fb).
  Keep units consistent; for example, convert kip-ft to kip-in when S is in
  in^3.
- Compare maximum absolute deflection with the user-selected span-to-deflection
  ratio, defaulting to L/360. Express span and deflection in the same units.
- Report reactions, maximum shear and moment, maximum bending stress, maximum
  deflection, and the applicable allowable values for each load case.

## Outputs
- For each load case, show the beam, supports, and applied loads, plus labeled
  shear, moment, and deflection diagrams with units and a documented sign
  convention.
- Report support reactions, maximum shear and moment with their locations,
  maximum bending stress, maximum deflection with its location, and the
  applicable allowable values.
- Show separate bending and deflection pass/fail results for each load case.

## Look and feel
- Use a clean, professional layout that groups inputs, the beam and load
  drawing, diagrams, and check results clearly.
- At the start of each visit, ask the user to choose Professional or Chaos mode
  before showing the beam workspace. Professional mode uses the standard clean
  palette; Chaos mode randomizes the app's color treatment and text font.
- Provide a header control to reopen the appearance chooser. Apply the choice
  for the current visit without saving it between visits.
- Open with the validation example already loaded.
- Label input units and show clear messages beside invalid inputs.
- Keep text, controls, and diagrams readable on both wide and narrow screens.

## Validation
- Reference case: a 20 ft simply supported W12x26 beam with a 1 kip/ft uniform
  load has a maximum moment of 50.0 kip-ft and a maximum deflection of 0.609 in.
- Record the W12x26 section and material properties, their source, the
  allowable bending stress, and the deflection limit used so the reference
  results are reproducible.
- Compare the reference moment within 0.05 kip-ft and deflection within
  0.0005 in, consistent with the precision shown above.
- Add hand-calculated cases for cantilevers, point loads, and multiple load
  cases. Record expected reactions, diagram extrema, deflection, stress, and
  pass/fail results for each numerical case.
- Verify that nonpositive spans and loads outside the beam are rejected with
  clear validation messages.

## Out of scope
- Continuous or multispan beams.
- Buckling or other stability checks.
- Shear-strength, torsion, and axial-load checks; the app displays a shear
  diagram but does not check shear capacity.
- Dynamic loading and connection design.
- Automatic code load combinations or load factors. User-defined load cases
  are analyzed separately and are not combined automatically.
