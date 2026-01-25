# NullSec JTAG Guide

## Overview
JTAG (Joint Test Action Group) debugging and exploitation toolkit.

## Hardware Setup

### Supported Adapters
| Adapter | Speed | SWD | JTAG |
|---------|-------|-----|------|
| FT2232H | 30 MHz | ✓ | ✓ |
| J-Link | 50 MHz | ✓ | ✓ |
| Bus Pirate | 1 MHz | ✓ | ✓ |
| Tigard | 24 MHz | ✓ | ✓ |
| Black Magic Probe | 4 MHz | ✓ | ✓ |

### Pin Identification
```bash
# Auto-detect JTAG pins
nullsec-jtag --scan --pins 1-20

# Known pinout
nullsec-jtag --connect --tck 1 --tms 2 --tdi 3 --tdo 4 --trst 5
```

## Operations

### Device Identification
```bash
# Read IDCODE
nullsec-jtag --idcode

# Scan chain
nullsec-jtag --scan-chain

# Boundary scan
nullsec-jtag --boundary-scan
```

### Memory Operations
```bash
# Dump flash
nullsec-jtag --read --addr 0x08000000 --size 0x100000 -o firmware.bin

# Write flash
nullsec-jtag --write --addr 0x08000000 -i modified.bin

# Erase flash
nullsec-jtag --erase --addr 0x08000000 --size 0x100000
```

### Debug Operations
```bash
# Halt CPU
nullsec-jtag --halt

# Read registers
nullsec-jtag --regs

# Single step
nullsec-jtag --step

# Set breakpoint
nullsec-jtag --break --addr 0x08001234

# Continue
nullsec-jtag --continue
```

## Common Targets

### ARM Cortex-M
```bash
nullsec-jtag --target cortex-m --connect --interface swd
```

### ARM Cortex-A
```bash
nullsec-jtag --target cortex-a --connect --interface jtag
```

### MIPS
```bash
nullsec-jtag --target mips --connect --ejtag
```

## Security Bypass

### Read Protection Bypass
```bash
# STM32 RDP bypass (voltage glitching)
nullsec-jtag --bypass rdp --method glitch --target stm32

# Debug authentication bypass
nullsec-jtag --bypass auth --method timing
```

### Secure Boot Bypass
```bash
nullsec-jtag --bypass secboot --extract-keys
```

## Legal Notice
For authorized hardware security research only.
