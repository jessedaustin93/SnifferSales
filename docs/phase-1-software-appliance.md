# Phase 1 Software Appliance Notes

This page mirrors the commercial-relevant parts of `Ethrox-Systems/ethrox-detect`
so the Ethrox Detect planning repo has the status without duplicating source
code.

## Source Of Truth

- Engineering repo: `https://github.com/Ethrox-Systems/ethrox-detect`
- Appliance branch: `codex/appliance-image`
- Release candidate: `v0.1.0-rc1`. The CI image build is green; a prerelease is
  published with a flashable `.img.xz` and its SHA-256 checksum.
- Current appliance prototype version: `0.2.0-rc.1+1`
- Product name in planning docs: Ethrox Detect.
- Historical/internal codename: SnifferOps.

## Appliance Components

- `linux/deploy/install-appliance.sh` - headless installer.
- `linux/deploy/ethrox-detect.service` - systemd service running the
  headless appliance.
- `linux/deploy/firstboot/` - one-shot first-boot provisioning.
- `linux/deploy/selftest.sh` - health / assembly test.
- `linux/deploy/durability/` - read-only-root hardening scripts.
- `image/` - pi-gen image build scaffolding.
- `.github/workflows/build-image.yml` - CI image build/release workflow.

## Current Validated Keep-Prototype Unit

- Hardware: Raspberry Pi Zero 2 W.
- API: port `8766`.
- Service: `ethrox-detect.service`.
- Hostname: `ethrox-detect-fffd49`.
- Wi-Fi IP during setup: `192.168.50.210`.
- USB rescue IP: `192.168.7.2`.
- Stable host USB interface: `enx02e0de7ec701`.

Validated on the flashed Pi:

- [x] service autostarts
- [x] API responds
- [x] node ID persists
- [x] Wi-Fi scanner works
- [x] onboard Bluetooth scanner works
- [x] RTL-SDR scanner works (USB dongle enumerated and accessible to the
  unprivileged service user; no antenna fitted, so pipeline only)
- [x] no-peripheral mode works
- [x] `selftest.sh` returns `RESULT: OK`
- [x] clean reboot validation passed
- [x] USB rescue route works
- [x] Wi-Fi route works
- [x] T5810B hub health and awareness GET routes are reachable
- [x] Pi imported the T5810B awareness snapshot during setup

Not yet validated:

- [ ] clean image rebuilt from latest appliance fixes and reflashed
- [ ] read-only-root/data-partition behavior on freshly flashed image
- [ ] destructive power-loss testing
- [ ] T5810B sync POST path
- [ ] RTL-SDR overnight validation with final antenna setup

## Current No-Peripheral Config

```json
{
  "port": 8766,
  "bind": "0.0.0.0",
  "wifi": true,
  "bluetooth": true,
  "sdr": false,
  "cellular": false,
  "sdr_remote": "",
  "peers": [
    {
      "host": "192.168.50.179",
      "port": 8766,
      "name": "t5810b-hub",
      "via": "wifi-lan"
    }
  ]
}
```

The systemd keep-prototype drop-in starts the service with:

```text
--peer 192.168.50.179:8766:t5810b-hub --plain
```

## Overnight Power-Only Test

The Pi is configured to run headlessly from a wall power source with no USB
computer connection.

- Timer: `ethrox-detect-overnight-sample.timer`
- Log path: `/var/lib/ethrox-detect/overnight/YYYYMMDD-power-only.jsonl`
- Sample cadence: every five minutes

Each sample records service state, failed units, Wi-Fi/USB addresses, local API
health, profile/type/class counts, and T5810B hub health.

Success for the first overnight run means the Pi remains online, scanning,
healthy, and able to reach the hub. It does not prove antennaed RTL-SDR
overnight behavior yet.

## T5810B Sync Limitation

The T5810B hub at `192.168.50.179:8766` currently responds to:

- `GET /ethrox-detect/health`
- `GET /ethrox-detect/version`
- `GET /ethrox-detect/awareness`

But `POST /ethrox-detect/sync` times out with no response, including for an
empty probe payload. Reliable push-to-hub sync is not proven until the T5810B
POST handler is debugged.

## Phase 1 Flash Test Checklist

The GitHub Actions image artifact is now available (`v0.1.0-rc1` prerelease), so
this checklist can be run against it:

- [ ] Download `.img.xz`.
- [ ] Download `.sha256`.
- [ ] Verify checksum.
- [ ] Flash image to SD card.
- [ ] Boot Pi Zero 2 W.
- [ ] Confirm SSH/admin access.
- [ ] Confirm hostname format follows the current appliance naming scheme.
- [ ] Confirm the appliance service is active.
- [ ] Confirm API responds on `:8766`.
- [ ] Confirm `/` is read-only or overlay-backed.
- [ ] Confirm `/var/lib/ethrox-detect` is writable and persistent.
- [ ] Confirm `node_id` persists across reboot.
- [ ] Confirm `config.json` exists and is valid.
- [ ] Confirm Wi-Fi scanner works.
- [ ] Confirm onboard Bluetooth scanner works.
- [ ] Run `sudo linux/deploy/selftest.sh` and get `RESULT: OK`.
- [ ] Run three clean reboot cycles.
- [ ] Only after clean reboot tests, consider controlled power-loss testing.

## Notes For Commercial Planning

Phase 1 proves the software appliance foundation. It does not prove a
sell-ready physical product, a case, battery runtime, antenna performance,
parts availability, pricing, website, support model, or fulfillment turnaround.
