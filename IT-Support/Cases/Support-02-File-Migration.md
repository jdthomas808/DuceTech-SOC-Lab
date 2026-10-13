# Support-02 — User File Migration and Handoff

**Date:** October 13, 2026
**Environment:** Windows 11 VM in VMware Workstation
**Exercise:** Folder-based migration simulation
**Status:** File transfer and handoff completed

## Objective
Practice preserving a user's document, checking it after
transfer, and documenting the result for another technician.

## Device Inventory
- Device name: DuceTech
- RAM: 4 GB
- Operating system: Windows 11 Pro
- Version: 25H2
- Available disk space: Approximately 36 GB

## Scenario
Jordan Davis, a fictional Operations employee, needs an
important document preserved during a workstation migration.

Three folders inside Documents represented the transfer stages:

- DuceTech-Employee-Files: Original employee files
- DuceTech-Migration-Staging: Temporary transfer location
- DuceTech-New-Workstation: Simulated destination

## Procedure
1. Created Employee-Report.txt with four lines of test content.
2. Copied the report from the original folder into staging.
3. Opened the staged copy and checked all four lines.
4. Copied the staged report into the destination folder.
5. Opened the destination copy and confirmed its contents.
6. Retained the original and staging copies.
7. Created Migration-Handoff.txt in the destination folder.
8. Reopened the handoff note to verify it was saved correctly.

## Verification
- The staged report opened with the expected text.
- The destination report opened with all four lines present.
- The original document was retained.
- The handoff note was saved in the destination folder.
- Screenshots were captured to document the result.

## Handoff Documentation
The handoff note recorded:
- Employee and device details
- The transferred filename
- Verification performed at each stage
- Retention of the original file
- The scope of the simulation
- Unresolved VM stability issues

## Outstanding Issue
The VM experienced unexpected restarts.

A CHKDSK online scan reported no file-system problems.
SFC found corrupt system files and could not repair some
of them. Further repairs were paused; the cause of the
restarts remains unconfirmed.

File-transfer verification succeeded, but workstation
stability was not confirmed.

## Scope and Limitations
This exercise used three folders on one VM's disk.
It did not perform a Windows upgrade, a complete user-profile
migration, or a transfer between separate computers.

The staging copy was a temporary holding copy, not an
independent backup against failure of the VM's disk.

## What I Learned
- Preserve the original until the destination is verified.
- Check file contents instead of assuming copying succeeded.
- Use staging when a transfer needs a temporary holding location.
- Document completed work and unresolved issues clearly.
- Distinguish successful file transfer from overall device readiness.

## Evidence
Screenshots will be added next.
