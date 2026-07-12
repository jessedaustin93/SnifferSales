# Phase 1 Software Appliance Notes

This page mirrors the commercial-relevant parts of `jessedaustin93/Sniffer-Ops`
so the sales/product repo has the status without duplicating source code.

## Source Of Truth

- Engineering repo: `https://github.com/jessedaustin93/Sniffer-Ops`
- Appliance branch: `codex/appliance-image`
- Current release candidate tag observed: `v0.1.0-rc1`

## Appliance Components

- `linux/deploy/install-appliance.sh` - headless installer.
- `linux/deploy/snifferops.service` - systemd service running
  `snifferops_linux.py --headless`.
- `linux/deploy/firstboot/` - one-shot first-boot provisioning.
- `linux/deploy/selftest.sh` - health / assembly test.
- `linux/deploy/durability/` - read-only-root hardening scripts.
- `image/` - pi-gen image build scaffolding.
- `.github/workflows/build-image.yml` - CI image build/release workflow.

## Current Validated Guinea-Pig Unit

- Hardware: Raspberry Pi Zero 2 W.
- Hostname: `snifferops-4a939c`.
- Node ID: `4a939c799f994421`.
- USB route: `192.168.7.2`.
- Wi-Fi route observed: `192.168.50.210`.
- API: port `8766`.
- Service: `snifferops.service`.

Validated on the hand-installed Pi:

- [x] service autostarts
- [x] API responds
- [x] node ID persists
- [x] Wi-Fi scanner works
- [x] onboard Bluetooth scanner works
- [x] no-peripheral mode works
- [x] `selftest.sh` returns `RESULT: OK`
- [x] three clean reboot cycles passed
- [x] no persistent journald directory

Not yet validated:

- [ ] CI-built `.img.xz` flashes and boots
- [ ] read-only-root/data-partition behavior on freshly flashed image
- [ ] destructive power-loss testing

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
  "peers": []
}
```

## Phase 1 Flash Test Checklist

Use this once the GitHub Actions image artifact is available:

- [ ] Download `.img.xz`.
- [ ] Download `.sha256`.
- [ ] Verify checksum.
- [ ] Flash image to SD card.
- [ ] Boot Pi Zero 2 W.
- [ ] Confirm SSH/admin access.
- [ ] Confirm hostname format `snifferops-<shortid>`.
- [ ] Confirm `snifferops.service` is active.
- [ ] Confirm API responds on `:8766`.
- [ ] Confirm `/` is read-only or overlay-backed.
- [ ] Confirm `/var/lib/snifferops` is writable and persistent.
- [ ] Confirm `node_id` persists across reboot.
- [ ] Confirm `config.json` exists and is valid.
- [ ] Confirm Wi-Fi scanner works.
- [ ] Confirm onboard Bluetooth scanner works.
- [ ] Run `sudo linux/deploy/selftest.sh` and get `RESULT: OK`.
- [ ] Run three clean reboot cycles.
- [ ] Only after clean reboot tests, consider controlled power-loss testing.

## Notes For Commercial Planning

Phase 1 proves the software appliance foundation. It does not prove a sell-ready
physical product, a case, battery runtime, antenna performance, parts
availability, pricing, website, support model, or fulfillment turnaround.
