# Ethrox Detect Planning

Commercial planning repo for **Ethrox Detect** productization, sales, hardware
SKUs, parts planning, cases, fulfillment, legal wording, and launch work.

This repo is separate from the engineering app repo:

- Software / appliance source: `Ethrox-Systems/ethrox-detect`
- Commercial planning: `Ethrox-Systems/ethrox-detect-planning`

`SnifferOps` and `SnifferSales` are retained only as historical/internal
codenames while the product line moves under the Ethrox Systems organization.

## Start Here

- [Product Roadmap / Checklist](docs/ethrox-detect-roadmap.md)
- [Phase 1 Software Appliance Notes](docs/phase-1-software-appliance.md)
- [Legal / Name Availability Check](docs/legal-name-check.md)
- [Public Product Name Brief](docs/public-name-brief.md)

## Current Framing

Phase 1 is the software appliance foundation: headless installer, reproducible
bootable image, read-only-root durability, CLI/service behavior, and Pi Zero 2 W
validation.

Sell-ready physical units, cases, peripherals, batteries, screens, antennas,
parts lists, pricing, website, and fulfillment are separate later phases.

Current keep-prototype status:

- Pi Zero 2 W keep-prototype is running Ethrox Detect `0.2.0-rc.1+1`.
- Wi-Fi route: `192.168.50.210`.
- USB rescue route: `192.168.7.2`.
- Overnight power-only validation is configured through an on-device timer.
- T5810B hub health/awareness GET routes work, but sync POST currently times
  out and needs engineering follow-up.
