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
### Standard User Account

<img width="540" height="270" alt="Screenshot 2026-10-13 173151" src="https://github.com/user-attachments/assets/331d5c0e-fe7f-46d1-a48a-af01e1945365" />

### Windows Update Findings

<img width="468" height="624" alt="Screenshot 2026-10-13 183200" src="https://github.com/user-attachments/assets/d6d87a2f-1da9-4061-8c95-ddd303221ec9" />

### Acceptance Checklist and Handoff Decision

<img width="1156" height="607" alt="Screenshot 2026-10-13 185317" src="https://github.com/user-attachments/assets/eb322792-55c6-49de-b426-0e55b8f50843" />

### Successful Printing from the Standard Account

<img width="454" height="602" alt="Screenshot 2026-10-13 182521" src="https://github.com/user-attachments/assets/fca80802-a9e4-4d9e-93a8-a9f2dac175d4" />

