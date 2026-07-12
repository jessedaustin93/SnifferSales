# SnifferOps Commercial Roadmap

Updated from the original Phase 1 installer/image plan on 2026-07-12.

## Purpose

Keep software appliance work, sell-ready hardware work, and go-to-market work
separate so each phase has a clear finish line.

The engineering repo remains the source of SnifferOps software:

- `https://github.com/jessedaustin93/Sniffer-Ops`

This commercial repo tracks productization and sales planning:

- `https://github.com/jessedaustin93/SnifferSales`

## Phase 1 - Software Appliance Foundation

Goal: produce and validate the software-only appliance build.

This phase is done when SnifferOps can be installed or flashed as a reproducible
headless appliance and verified on a Pi Zero 2 W class target.

### Scope Checklist

- [x] Headless installer: `linux/deploy/install-appliance.sh`.
- [ ] `.deb` or packaged installer, if we decide it is needed.
- [ ] Flashable OS image: `snifferops-os-vX.img.xz`.
- [x] System service: `snifferops.service`.
- [x] Stable node identity and config under `/var/lib/snifferops`.
- [x] No-GTK appliance path using `snifferops_linux.py --headless`.
- [x] First-boot provisioning.
- [x] Read-only-root or overlay-root durability implemented in repo.
- [ ] Read-only-root flashed-image validation on real Pi.
- [x] Writable SnifferOps data path planned under `/var/lib/snifferops`.
- [x] Self-test script for assembly and image validation.
- [ ] CI image build publishes image and checksum artifacts.

### Acceptance Checklist

- [ ] CI image builds successfully.
- [ ] `.img.xz` and `.sha256` are available and verify cleanly.
- [ ] Image boots on a Pi Zero 2 W from a freshly flashed card.
- [x] SSH/admin access works on the hand-installed guinea-pig Pi.
- [x] `snifferops.service` starts automatically on the hand-installed Pi.
- [x] API answers on port `8766` on the hand-installed Pi.
- [x] Node ID persists across reboot on the hand-installed Pi.
- [x] Wi-Fi and onboard Bluetooth scanning work without extra peripherals.
- [x] SDR/cellular are disabled unless hardware is present.
- [x] `selftest.sh` returns `RESULT: OK` on the hand-installed Pi.
- [x] Three clean reboot cycles pass on the hand-installed Pi.
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

## Phase 2 - Commercial Repo And Product Definitions

Goal: turn the working software appliance into a product plan without committing
to hardware inventory too early.

### Scope Checklist

- [x] Keep this `SnifferSales` repo as the commercial planning home.
- [ ] Pick a public commercial name to replace `SnifferOps`.
- [ ] Complete legal/name availability clearance.
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

- [ ] Let the current CI image build finish.
- [x] Do not add new feature scope until the image is tested.
- [x] Prepare the flash/test checklist.
- [x] Keep the current Pi guinea-pig running as the known-good baseline.
- [ ] When the artifact is ready, flash a card and validate the Phase 1 acceptance
  checklist before declaring Phase 1 complete.

## Open Decisions

- [ ] Commercial repo structure after this initial roadmap.
- [x] Decision: `SnifferOps` should not be the public commercial brand. See
  [Legal And Name Availability Check](legal-name-check.md).
- [ ] New public product name and branding status. See
  [Public Product Name Brief](public-name-brief.md).
- [ ] Whether the first public offering is image-only, kit, or assembled unit.
- [ ] Default admin username for public images.
- [ ] Wi-Fi onboarding method for customers.
- [ ] Which peripherals are mandatory for each SKU.
- [ ] Whether portable units include a battery in early sales or stay USB-powered.
- [ ] Whether a screen is standard, optional, or deferred.
