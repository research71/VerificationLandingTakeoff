# ProB animation scenarios (Dublin)

Each scenario animates `M4_Dublin` with ProB on the data of `C4_Dublin` and reaches one of the six critical cases (CS1 to CS6). In each capture, an event with a red icon is disabled and an event with a green triangle is enabled. In the captures, ProB writes `AIRCRAFTSN` for the aircraft that the paper calls `A_N`.

| Case | Requirement | Event | Guard / invariant | Situation | Expected result |
|---|---|---|---|---|---|
| CS1 | R1 | `Entry_in_TMA` | `grd10`, `grd11`, `grd13`, `act8`; `inv7` (M2) | Three Light aircraft enter through OSGAR | Entry times 0, 82, 164 (gap 82 s = `Separation_time(Light ↦ Light)`); invariants ok |
| CS2 | R2 | `Direct_To` | `grd7`; `inv19` (M2) | A6 (Heavy) behind A8 (Heavy) on LEG_N | Disabled at 999 s (would reach LAPMO at 1242 < 1259); enabled at 1051 s, `mergeTime(A6) = 1294` |
| CS3 | R3 | `Touchdown` | `grd9`; `inv16` (M4) | A9 (Medium) lands, then A8 (Heavy) | Disabled until 1463 + 60 = 1523 s, then enabled |
| CS4 | R4 | `Touchdown` | `inv5`, `inv6` (M0, M1) | Runway status and lights | Available/OFF before, Unavailable/ON after, simultaneously; invariants ok |
| CS5 | R5 | `Touchdown`, `Start_takingoff` | `grd7` of `Touchdown`, `grd6` of `Start_takingoff`; `inv17`, `inv18` (M4) | Take-off then landing, and landing then take-off | Landing enabled at 2177 + 60 = 2237 s; take-off disabled at 2374 s (gap 34 s), enabled at 2340 + 60 = 2400 s |
| CS6 | R6 | `Start_takingoff` | `grd5`; `inv19` (M4) | A9 (Medium) takes off, then A8 (Heavy) | Disabled until 2057 + 60 = 2117 s, then enabled |

## Contents

- `captures/`: full-size ProB captures, named `CSn_*`.
- `traces/`: ProB traces (`*.prob2trace`) that replay each scenario in ProB2-UI (`Load trace`).

## Replaying a scenario

1. Open `Verif/M4_Dublin` in Rodin with ProB, or load the machine in ProB2-UI.
2. Set `DEFAULT_SETSIZE` to 9 so that the abstract set `AIRCRAFTS` has enough elements for the scenario.
3. Start with `SETUP_CONTEXT`, then `INITIALISATION`.
4. Load the trace of the case in the `Trace` view and replay it.
