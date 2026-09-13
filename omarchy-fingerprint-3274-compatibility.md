# Add Microarray vendor `3274` to Omarchy fingerprint detection

## Tested hardware

- USB ID: `3274:8012`
- Device: MicroarrayTechnology MAFP General Device
- Product: TNP Nano USB Fingerprint Reader

## Tested software

```text
libfprint 1.94.100-1
fprintd   1.94.5-2
```

The device works with the stock Arch fingerprint stack.

## Enrollment and verification

```bash
fprintd-enroll -f right-index-finger "$USER"
# Enroll result: enroll-completed

fprintd-verify "$USER"
# Verify result: verify-match (done)
```

## Omarchy change

The current vendor list omits `3274`:

```bash
fingerprint_vendors=" 27c6 138a 06cb 08ff 1c7a 147e "
```

Proposed one-line change:

```diff
-fingerprint_vendors=" 27c6 138a 06cb 08ff 1c7a 147e "
+fingerprint_vendors=" 27c6 138a 06cb 08ff 1c7a 147e 3274 "
```

After adding `3274`, `Setup → Security → Fingerprint` appears. The normal Omarchy fingerprint setup then completes successfully, and fingerprint authentication works through the Omarchy integration.

Testing is specific to `3274:8012`; this report does not claim that all vendor-`3274` devices are supported.


