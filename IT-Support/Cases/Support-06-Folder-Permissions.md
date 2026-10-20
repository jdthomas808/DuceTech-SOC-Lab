# Support-06: Local Folder Access and Least Privilege

## Simulated Ticket
- Ticket ID: LAB-006
- Subject: Jordan Davis cannot access the Operations notice.
- Requester: Jordan.Davis
- Category: Access / Local folder permissions
- Impact: One user cannot read one Operations notice.
- Urgency: No immediate deadline specified in the scenario.
- Status: Resolved after access verification.
- Environment: DuceTech Windows 11 VM.
- Resource: C:\DuceTech-Shared\Team-Notice.txt

This was a controlled lab using local NTFS permissions.
No network share or production ticketing application was used.

## Objective
Troubleshoot folder access and restore only the permissions
needed to read a notice, while preventing unauthorized changes.

## Baseline and Controlled Fault
Created the practice folder and Operations notice.
Confirmed Jordan could initially open the notice.

Disabled inheritance on the practice folder and converted
inherited permissions into explicit entries.

Removed Users entries, but Jordan still had access.
Inspected the permissions with:

    icacls "C:\DuceTech-Shared"

Authenticated Users still had Modify permission.
Removed that entry while retaining Administrators and SYSTEM.

Signed in as Jordan and confirmed folder access was blocked.

## Investigation and Work Notes
Attempted to grant Jordan Read & execute through the Security UI.
Windows displayed an access-denied error while applying permissions.

An elevated Command Prompt later confirmed the folder contained:
- Administrators: Full control
- SYSTEM: Full control
- Jordan.Davis: Read & execute

The folder result alone did not confirm access to the notice.

The initial file-permission query failed because the filename
was Team-Notice.txt.txt. Listed the directory to identify the
actual name, then renamed the file to Team-Notice.txt.

Checked the file permissions:

    icacls "C:\DuceTech-Shared\Team-Notice.txt"

The file listed Administrators and SYSTEM, but no Jordan entry.
The cause of the earlier UI error was not conclusively established.

## Corrective Action
Granted Jordan Read permission on the specific notice:

    icacls "C:\DuceTech-Shared\Team-Notice.txt" /grant "DuceTech\Jordan.Davis:R"

Result:
Successfully processed 1 files; Failed processing 0 files.

Retained administrator and SYSTEM access.
Did not grant Jordan Modify, Full control, or administrator membership.

## Verification
Signed in as Jordan.Davis and verified:

| Test | Result |
|---|---|
| Open Team-Notice.txt and read its original text | Passed |
| Create Jordan-Write-Test.txt in the folder | Access denied, as intended |
| Append text to Team-Notice.txt | Access denied, as intended |

Creation test:

    echo Permission test > "C:\DuceTech-Shared\Jordan-Write-Test.txt"

Modification test:

    echo Permission test>>"C:\DuceTech-Shared\Team-Notice.txt"

Both write attempts were denied.

## Resolution Notes
Restored access to the Operations notice for Jordan.Davis.
Verified read access using the affected standard-user account.
Verified that creating files and modifying the notice remained blocked.

## Simulated User Update
Your access to the Operations notice has been restored.
You can open and read it. Editing the notice and adding files
remain restricted because this access is intended for viewing only.

## Evidence
- Notice accessible before the controlled fault.
  <img width="1117" height="582" alt="Screenshot 2026-10-16 150630" src="https://github.com/user-attachments/assets/1be48928-02eb-438c-a29a-ccb7fa1027a8" />

- Folder access blocked as Jordan.
  <img width="1119" height="589" alt="Screenshot 2026-10-16 163142" src="https://github.com/user-attachments/assets/6a56b75d-a823-4041-8554-518e54840020" />

- Folder and file permission command output.
  <img width="972" height="504" alt="Screenshot 2026-10-16 165725" src="https://github.com/user-attachments/assets/36d9edfb-a141-4fa1-b53a-2b957ae78d89" />

- Notice readable after the correction.
  <img width="1702" height="905" alt="Screenshot 2026-10-20 180714" src="https://github.com/user-attachments/assets/7bcdbdf4-3c07-48fb-9eaa-f2aa30c2c6a4" />

- File creation denied & Notice modification denied.
  <img width="1118" height="618" alt="Screenshot 2026-10-20 181047" src="https://github.com/user-attachments/assets/4e347de1-f322-4ea5-b9ad-e36f747b0e27" />


## Lessons Learned
- Group permissions can grant access even without a direct user entry.
- Removing Users did not remove access through Authenticated Users.
- Check permissions on both the folder and the affected file.
- Verify access using the affected user's account.
- Test both the required access and the restrictions that should remain.

## Separate Outstanding Issue
Recurring VM crashes interrupted the exercise and remain unresolved.
They were not established as the cause of the permission issue.
