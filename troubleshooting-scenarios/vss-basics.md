# VSS Basics and Writer Health Check

## What is VSS?
Volume Shadow Copy Service (VSS) is a Windows subsystem responsible for taking consistent snapshots. Acronis relies on VSS for image-level backups.

## Key Commands
- `vssadmin list writers`
- `vssadmin list providers`
- `vssadmin list shadows`

## Writer States
- **Stable (OK)**
- **Retryable Error**
- **Non-retryable Error**
- **Waiting for Completion**
- Missing writer (not listed)

## Common Causes of VSS Issues
- Application writer failure (SQL, Hyper-V, System Writer)
- Corrupted VSS components
- Permission issues
- Stalled shadow copies
- Failed VSS/SwPrv services

## Initial Troubleshooting Steps
1. Check writer states
2. Restart:
   - `net stop swprv`
   - `net stop vss`
   - `net start vss`
   - `net start swprv`
3. Review Event Viewer for VSS and application errors
