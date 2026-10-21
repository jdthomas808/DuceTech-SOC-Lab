# Simulation 01: Replacement Workstation Deployment

## Environment
- Platform: ServiceDesk Simulator
- Practice type: Simulated service desk ticket and workstation deployment
- User: Quinn Adams
- Department: Customer Support
- Location: Floor 1
- Replacement workstation: SD2036
- Status: Replacement prepared and assigned; delivery and user validation pending

## Reported Issue and Business Impact
Quinn reported that his desktop would not power on. There were no lights, fan activity, or audible beeps.

He could not handle customer calls, causing work to queue.

## Initial Troubleshooting
The user confirmed:
- The wall outlet worked with another device.
- The power cable was secure at both ends.
- The power strip was switched on.
- Pressing the power button did not start the desktop.

The specific hardware fault was not established.

## Service Restoration Approach
Prioritized preparing a replacement workstation so Quinn could return to handling calls.

Selected Server Imaging because the deployment documentation identified the Customer Support softphone as requiring this method.

## Deployment Actions
1. Consulted the deployment standard operating procedure.
2. Checked the asset register and identified SD2036 as the next available identifier.
3. Selected PXE Network Boot IPv4.
4. Authenticated to the Deployment Wizard using the documented deployment credentials.
5. Set OSDComputerName to SD2036.
6. Ran the corporate imaging task sequence.
7. Verified technician domain sign-in after imaging.
8. Registered SD2036 in Asset Management.
9. Assigned SD2036 to Quinn Adams and marked it Deployed in inventory.

## Sign-In Issue Encountered
The initial technician sign-in attempts were rejected.

Comparing the displayed credentials with the entered username revealed a difference between a curly apostrophe and a straight apostrophe. Copying the exact displayed username allowed sign-in.

Lesson: Visually similar characters can differ. Compare the exact account identifier before changing account settings or passwords.

## Verification Completed
- Technician domain sign-in succeeded.
- Asset tag and hostname both showed SD2036.
- Asset Management showed Quinn Adams as the assigned user.
- Inventory status showed Deployed.

## Remaining Actions
- Complete replacement delivery through Ship Manager.
- Confirm Quinn can sign in.
- Confirm the Customer Support softphone works and Quinn can handle calls.
- Record or route the original desktop for hardware assessment.

The inventory status alone does not confirm delivery or restored service.

## Evidence
Screenshots to add:
1. Ticket and resolution notes:
   <img width="665" height="513" alt="Screenshot 2026-10-20 205028" src="https://github.com/user-attachments/assets/b8eb8f20-2cca-4489-abe1-6209a4471f3b" />

2. Simulator’s expected solution:
   <img width="625" height="512" alt="Screenshot 2026-10-20 205305" src="https://github.com/user-attachments/assets/c9b81de4-1cdc-428c-b7f7-1f9cdb57ef56" />

3. SD2036 asset record:
   <img width="652" height="249" alt="Screenshot 2026-10-20 205627" src="https://github.com/user-attachments/assets/a8358590-4440-4358-b2a7-d63c935bb104" />


Exclude passwords and credential banners from published screenshots.

## Skills Practiced
- User communication and business-impact assessment
- Selecting a deployment method from company documentation
- PXE boot and automated workstation imaging
- Computer naming and asset registration
- Troubleshooting sign-in input
- Accurate ticket documentation and verification
