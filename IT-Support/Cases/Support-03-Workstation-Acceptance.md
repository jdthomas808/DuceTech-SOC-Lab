# Support-03 — Standard User Setup and Workstation Acceptance

**Date:** October 13, 2026
**Environment:** Windows 11 VM in VMware Workstation
**Exercise:** Controlled workstation setup and acceptance testing
**Status:** Assessment completed; workstation handoff on hold

## Objective
Create a standard employee account, test basic work tasks,
and document whether the workstation is ready for handoff.

## Device and Test User
- Device: DuceTech
- OS: Windows 11 Pro, version 25H2
- RAM: 4 GB
- Fictional employee: Jordan Davis
- Local account: Jordan.Davis
- Account type: Standard User

## Account Setup
1. Created a local account through Settings → Accounts → Other users.
2. Confirmed the account type was Standard User.
3. Signed out of the existing account.
4. Signed in as Jordan.Davis and allowed Windows to prepare the profile.

Standard-user access supports everyday work while limiting
administrative changes.

## Acceptance Tests

| Test | Observed result | Outcome |
|---|---|---|
| Sign in as Jordan.Davis | Desktop loaded successfully | Passed |
| Open Notepad | Application opened | Passed |
| Save a document | Workstation-Test.txt saved in Jordan's Documents | Passed |
| Reopen the document | Both test lines displayed | Passed |
| Browse the web | Microsoft website loaded in Edge | Passed |
| Print to PDF | Jordan-Print-Test.pdf opened with the expected text | Passed |
| Check Windows Update | Missing security updates and an installation error reported | Not passed |

## Update Findings
At the time of inspection:
- KB5129195 showed Installing — 0%.
- KB5126052 (.NET Framework) showed install error 0x800706ba.
- Windows reported missing important security updates.

Successful update installation was not verified.

## Outstanding Stability Issue
The VM had experienced unexpected restarts.
An earlier SFC scan found corrupt system files it could not
fully repair. The cause of the restarts remains unconfirmed,
and further repairs were paused.

## Handoff Decision
**Hold pending update and stability resolution.**

Basic employee tasks passed, but those results do not establish
that the entire workstation is ready for deployment.

In a workplace, I would record the failed checks and refer the
unresolved issues to the appropriate technician or deployment lead.
No actual workplace escalation occurred in this lab.

## Documentation
Created Workstation-Acceptance-Checklist.txt in Jordan's Documents.
Reopened it to verify it was saved and recorded:
- Passed user tests
- Update findings
- Unresolved stability issues
- The decision to hold handoff

## Scope and Limitations
This case demonstrates local standard-user account setup and
acceptance testing in an existing Windows 11 VM.

It does not demonstrate an OS installation, Windows 10-to-11
upgrade, enterprise account provisioning, or successful repair
of the update and stability issues.

## What I Learned
- Test everyday tasks from the employee's account.
- Confirm saved documents and printed output are usable.
- Record actual update status rather than assuming readiness.
- Separate successful individual tests from overall deployment approval.
- Document unresolved issues and make a clear handoff decision.

## Evidence
Screenshots will be added next.
