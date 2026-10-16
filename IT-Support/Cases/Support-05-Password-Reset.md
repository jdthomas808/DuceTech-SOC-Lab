# Support-05: Local Account Password Reset and Recovery

**Environment:** DuceTech Windows 11 VM  
**Account:** Jordan.Davis — local standard user  
**Status:** Password reset and access verification completed

## Objective
Practice an administrator-assisted password reset for a local
Windows account, then verify sign-in and file access.

## Scenario
Simulated a user forgetting their password.
This was a controlled lab exercise, not an actual forgotten-password incident.

In a workplace, verify the requester's identity and authorization
according to organizational procedures before resetting a password.

## Initial Account Check
From an elevated Command Prompt, ran:

    net user Jordan.Davis

Confirmed:
- Account active: Yes
- Local group membership: Users
- User may change password: Yes

## Troubleshooting
The Local Users and Groups tool was blocked from opening.
Settings confirmed the support account was an administrator.
Used an elevated Command Prompt to perform the reset.

The cause of the application block was not established.

## Corrective Action
Ran:

    net user Jordan.Davis *

Entered and confirmed a new lab-only password using the hidden
password prompts.

Windows reported: "The command completed successfully."

Administrator-assisted resets can affect encrypted files and
stored credentials. Passwords were kept private.

## Verification
- Signed out of the administrator account.
- Signed in to Jordan.Davis using the new password.
- Opened Workstation-Test.txt and confirmed its original text remained.
- Created Support-05-Access-Test.txt in Documents.
- Closed and reopened the new file; confirmed the saved text remained.

## Outcome
New-password sign-in and the tested file operations succeeded.
Jordan.Davis retained the standard-user setup; no administrator
membership was granted during the exercise.

This exercise covered a local Windows account.
Microsoft 365 and domain account resets were outside its scope.

## Separate Outstanding Issue
Recurring VM crashes remain unresolved.
A crash occurred before the reset; the reset and access checks
were subsequently completed.

## Evidence
1. Before-reset account details were recorded as command output:
   - Account active: Yes
   - Local group membership: Users
   - User may change password: Yes
   - Password last set: October 13, 2026, at 5:21:27 PM
     
2. Successful password reset command.
   <img width="979" height="500" alt="Screenshot 2026-10-15 195854" src="https://github.com/user-attachments/assets/8b3de628-04f4-427e-8f25-62670b2b3b0d" />

3. Existing document accessible after reset.
   <img width="1199" height="618" alt="Screenshot 2026-10-15 201755" src="https://github.com/user-attachments/assets/adcb94b5-dac9-4789-bb1f-74ef281fbbe7" />

4. New document reopened successfully after saving.
   <img width="1145" height="620" alt="Screenshot 2026-10-15 201833" src="https://github.com/user-attachments/assets/de64b651-a5f8-4934-9022-c6d5b64262cf" />


## Lesson Learned
Confirm the target account before making changes.
Verify successful sign-in and the user's ability to resume work
before closing a password-reset case.
