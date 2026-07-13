# Ethrox Detect Product Roadmap

Updated from the original Phase 1 installer/image plan on 2026-07-12.

## Purpose

Keep software appliance work, sell-ready hardware work, and go-to-market work
separate so each phase has a clear finish line.

The engineering repo is the source of the appliance software:

- `https://github.com/Ethrox-Systems/ethrox-detect`

This planning repo tracks Ethrox Detect productization and sales planning:

- `https://github.com/Ethrox-Systems/ethrox-detect-planning`

Historical note: this product was planned under the `SnifferOps` and
`SnifferSales` codenames before moving under Ethrox Systems.

## Phase 1 - Software Appliance Foundation

Goal: produce and validate the software-only appliance build.

This phase is done when Ethrox Detect can be installed or flashed as a
reproducible headless appliance and verified on a Pi Zero 2 W class target.

### Scope Checklist

- [x] Headless installer: `linux/deploy/install-appliance.sh`.
- [ ] `.deb` or packaged installer, if we decide it is needed.
- [x] Flashable OS image: `ethrox-detect-os-0.2.0-rc.1-build.1.img.xz`.
- [x] System service: `ethrox-detect.service`.
- [x] Stable node identity and config under the appliance data directory.
- [x] No-GTK appliance path using the current headless runner.
- [x] First-boot provisioning.
- [x] Read-only-root or overlay-root durability implemented in repo.
- [ ] Read-only-root flashed-image validation on real Pi.
- [x] Writable appliance data path planned.
- [x] Self-test script for assembly and image validation.
- [ ] CI image build publishes image and checksum artifacts.

### Acceptance Checklist

- [x] Local pi-gen image builds successfully.
- [x] `.img.xz` and SHA-256 are available and verify cleanly.
- [x] Image boots on a Pi Zero 2 W from a freshly flashed card.
- [x] SSH/admin access works on the keep-prototype Pi.
- [x] Current system service starts automatically on the keep-prototype Pi.
- [x] API answers on port `8766` on the keep-prototype Pi.
- [x] Node ID persists across reboot on the keep-prototype Pi.
- [x] Wi-Fi and onboard Bluetooth scanning work without extra peripherals.
- [x] SDR/cellular are disabled unless hardware is present.
- [x] `selftest.sh` returns `RESULT: OK` on the hand-installed Pi.
- [x] Three clean reboot cycles pass on the hand-installed Pi.
- [ ] Rebuild and reflash from the latest appliance fixes so the image does not
  rely on live card repairs.
- [ ] Read-only/overlay root and writable data partition behavior are confirmed
  on a freshly flashed CI image.
- [ ] Controlled power-loss testing passes on read-only image.
- [x] No private credentials, keys, raw public keys, GPS histories, captures, or
  DBs are committed.

### Not Phase 1

- [ ] Saleable enclosure design.
- [ ] Batteries, screens, antennas, SDR modules, or SKU parts selection.
- [ ] Printed case manufacturing.
- [ ] Pricing.
- [ ] Website.
- [ ] Payment processing.
- [ ] Fulfillment or turnaround-time promises.
- [ ] Support policy.

## Phase 2 - Product Definitions

Goal: turn the working software appliance into a product plan without committing
to hardware inventory too early.

### Scope Checklist

- [x] Transfer planning repo to Ethrox Systems.
- [x] Rename planning repo to `ethrox-detect-planning`.
- [x] Reframe the public product line as Ethrox Detect.
- [ ] Complete legal/name availability clearance for Ethrox Detect.
- [ ] Define product names and rough SKU ladder.
- [ ] Decide what is included in each model.
- [ ] Track parts, vendors, price ranges, lead times, and substitutions.
- [ ] Separate mandatory parts from optional/performance parts.
- [ ] Define what claims each SKU can honestly make.
- [ ] Keep legal/safety wording aligned with passive defensive awareness.

### Likely SKU Families

- [ ] Software-only image / installer.
- [ ] Basic Pi appliance: Wi-Fi + onboard Bluetooth only.
- [ ] SDR model: Pi appliance plus RTL-SDR and antenna.
- [ ] Portable model: battery, case, optional small screen, antennas.
- [ ] Lab/station model: powered enclosure, better antenna layout, maybe Ethernet.

Each SKU should have its own parts list, build time, support burden, and margin
estimate before any public promise is made.

### Acceptance Checklist

- [ ] Initial SKU matrix exists.
- [ ] Each SKU has a bill of materials draft.
- [ ] Each SKU has known blockers and unknowns.
- [ ] No SKU depends on unavailable or untested parts.
- [ ] Hardware claims are tied to tested configurations.

## Phase 3 - Sell-Ready Hardware Unit

Goal: design and validate physical units that can be built repeatedly.

This is its own phase because hardware will change cost, case design, testing,
support, and fulfillment timelines.

### Scope Checklist

- [ ] Case design and print tests.
- [ ] Mounting for Pi, screen, SDR, antennas, battery, switches, and ports.
- [ ] Thermal checks.
- [ ] Power stability checks.
- [ ] Battery/runtime testing if portable.
- [ ] Antenna placement testing.
- [ ] Screen/UI fit if a display SKU exists.
- [ ] Cable strain relief, especially for fragile micro-USB connections.
- [ ] Assembly steps and QA checklist.
- [ ] Parts list with vendor links and fallback parts.

### Acceptance Checklist

- [ ] At least one complete sell-ready prototype exists.
- [ ] Case prints reliably.
- [ ] Parts fit without fragile pressure points.
- [ ] Power is stable through movement.
- [ ] SD card survives repeated restart/power tests for the intended use case.
- [ ] Assembly can be repeated from a written checklist.
- [ ] Self-test passes on the final hardware configuration.
- [ ] Build time and part cost are known.

## Phase 4 - Marketing, Sales, And Fulfillment

Goal: go from no public sales presence to a minimal credible sales operation.

### Scope Checklist

- [ ] Website or landing page.
- [ ] Product positioning and copy.
- [ ] Safety/legal boundaries.
- [ ] Screenshots or photos of real tested hardware.
- [ ] SKU descriptions and honest feature lists.
- [ ] Pricing model.
- [ ] Payment flow.
- [ ] Shipping/turnaround-time policy.
- [ ] Inventory and part availability tracking.
- [ ] Support channel and warranty/return policy.
- [ ] Basic documentation for buyers.

### Acceptance Checklist

- [ ] Landing page exists.
- [ ] Each listed product maps to a tested SKU.
- [ ] No product claim outruns tested hardware.
- [ ] Estimated turnaround times are based on real part availability.
- [ ] Buyer setup instructions exist.
- [ ] Support/return boundaries are written before taking orders.

## Immediate Work While Phase 1 Builds

- [x] Build and flash the current local pi-gen image.
- [x] Do not add new feature scope until the image is tested.
- [x] Prepare the flash/test checklist.
- [x] Keep the current Pi keep-prototype running as the known-good baseline.
- [x] Configure power-only overnight logging.
- [ ] Review the power-only overnight run.
- [ ] Attach RTL-SDR and repeat overnight validation.
- [ ] Debug T5810B `POST /ethrox-detect/sync` timeout.
- [ ] Rebuild and reflash from the latest appliance fixes before declaring
  Phase 1 complete.

## Open Decisions

- [ ] Final commercial repo structure after this initial roadmap.
- [x] Decision: `SnifferOps` should not be the public commercial brand. See
  [Legal And Name Availability Check](legal-name-check.md).
- [x] Public product name selected for current planning: Ethrox Detect. See
  [Public Product Name Brief](public-name-brief.md).
- [ ] Whether the first public offering is image-only, kit, or assembled unit.
- [ ] Default admin username for public images.
- [ ] Wi-Fi onboarding method for customers.
- [ ] Which peripherals are mandatory for each SKU.
- [ ] Whether portable units include a battery in early sales or stay USB-powered.
- [ ] Whether a screen is standard, optional, or deferred.
