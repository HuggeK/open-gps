## Summary

Upgrade open-gps from the NEO-M9N to a u-blox ZED-X20P (Galileo HAS, decimetre accuracy without a base station) and add a pole so the unit can measure pin and ball positions. This builds on the roadmap's internal-antenna item.

![Pin probe, side view: antenna on a steel ground plate, electronics bay below, 5/8" hub, pole with bubble level, club ferrule in the cup](https://raw.githubusercontent.com/HuggeK/open-gps/docs/pin-probe-image/docs/images/pin-probe-side-view.png)

## Design

- **Stacked head:** all-band antenna on top (it must cover Galileo E6 for HAS, e.g. u-blox ANN-MB2), with no extra dome: its own housing is the only cover. A ~100 mm steel plate under it acts as ground plane, shield and mount. The X20, ESP32-S3 and 2 Ah battery sit in a printed bay below.
- **RF rules:** metal under the antenna helps; metal above or beside it hurts. No carbon-fibre, metal or glitter filaments, screws or foil near the antenna. The ESP32's 2.4 GHz antenna and the charger stay below the plate.
- **Antenna retention:** magnet plus a printed clip or screw, so a knock in the bag can't pull it off.
- **Mount:** 5/8"-11 UNC metal hub at the plate's centre (the standard survey thread), never a thread cut into plastic. Antenna centre, plate centre and thread on one axis, so readings are taken straight above the pole.
- **Bay:** the SparkFun ZED-X20P breakout (43.2 × 43.2 mm, Qwiic, SMA) replaces the NEO-M9N on the same Qwiic chain. Slide-in rails; display and dial move to a side face.
- **Pole:** ~1.3–1.4 m so the antenna clears the driver head in the bag. The club's own flagstick ferrule at the bottom centres it in the cup. Circular bubble level (1° of lean ≈ 2.4 cm at 1.4 m) and a survey quick release.
- **Pins:** press → about 5 s to step back 1–2 m (your body blocks GNSS) → 15–30 s average → buzz.
- **Shots:** stand the bag so the antenna is visually over the ball, step back, 5–10 s average (~20–40 cm, fine for shot distances). No tilt or compass sensor needed.
- **Power:** about 0.4 W on BLE, so the 2 Ah pack covers a round. The receiver stays on all round so HAS stays converged (a restart costs ~10 min).

## Plan

**Phase 1: X20 in the current case, antenna on the pole**

- [ ] Swap in the ZED-X20P breakout, flash the latest -01B firmware, enable Galileo HAS
- [ ] Antenna head: steel plate, all-band antenna, 5/8" hub, retaining clip
- [ ] Pole: ferrule adapter, rod, bubble level, quick release
- [ ] BLE output to a phone plus the capture routine (countdown, average, buzz)

**Phase 2: integrated head**

- [ ] OpenSCAD case as a bay with a plate groove on top and the antenna exposed above it, display on a side face
- [ ] X20, ESP32 and battery on slide-in rails below the plate

## Tests

1. Signal strength per band, including E6, with and without the ground plate
2. Self-interference: the same with BLE active and idle; watch the jamming indicator
3. HAS accuracy and time to 20 cm on a PPK-surveyed point
4. Centring: the same cup 10 times, rotating 90° each time; repeat with a person beside the probe vs 2 m away
5. Full-round battery runtime on a cold morning
6. Five greens against an RTK reference

## Open questions

- Does the ANN-MB2 cover E6, and what ground-plane size does u-blox recommend?
- How mature is HAS on the X20-01B firmware?
- Ferrule sizes differ (standard vs tournament): measure the club's cups first
- Does the Thing Plus charger block charging below 0 °C?
- Is a 1.3–1.4 m pole with the head on top too top-heavy for the bag and the cup?
- Club permission before golfers put probes in cups
