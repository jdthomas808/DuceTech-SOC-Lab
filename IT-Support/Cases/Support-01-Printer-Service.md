# Support-01 — Windows Print Spooler Troubleshooting

**Environment:** Windows 11 VM in VMware Workstation  
**Exercise:** Controlled lab simulation  
**Status:** Printing restored and verified  
**Date:** October 10–11, 2026

## Objective
Investigate a printing failure, restore service operation,
and verify that a new PDF opens and displays correctly.

## Working Baseline
- Created a VMware snapshot before making changes.
- Printed a test sentence from Notepad using Microsoft Print to PDF.
- Opened the PDF and confirmed the text displayed.
- Confirmed Spooler was Running in Task Manager.

## Controlled Fault and Symptoms
I deliberately stopped Spooler inside the VM.

Afterward:
- Notepad's print dialog remained loading.
- Task Manager confirmed Spooler was Stopped.
- A printer warning appeared with an empty printer list,
  asking whether to install a printer.

## Investigation and Recovery
1. Started Spooler through Task Manager.
2. Confirmed its status changed to Running.
3. Reopened the print dialog; Microsoft Print to PDF appeared.
4. Attempted to create a recovery PDF.
5. Edge and Chrome could not open that file.
6. Checked its Properties and found it contained 0 bytes.
7. Closed and reopened Notepad, entered new test text,
   and printed to a new PDF filename.
8. Opened the new PDF and confirmed the text displayed.

## Findings
Stopping Spooler caused the controlled printing disruption.

The first recovery PDF was empty. Its exact cause was not
established. A fresh Notepad session and a new print attempt
successfully produced a readable PDF.

## Additional Observation
Windows blocked mmc.exe when I attempted to open services.msc.
I used Task Manager's Services tab to inspect and control Spooler.
The cause of the MMC block was not diagnosed during this exercise.

## Verification
The final PDF opened and displayed the expected test sentence.
A screenshot was captured as recovery evidence.

## What I Learned
- Establish a working baseline before changing a system.
- Check service status when investigating printing problems.
- A service showing Running does not prove the user's task works.
- A file existing does not prove it contains usable data.
- Verify recovery by repeating the task and opening the output.
- Document uncertain causes without presenting guesses as facts.

## Evidence
<img width="474" height="623" alt="Screenshot 2026-10-10 134114" src="https://github.com/user-attachments/assets/7420042b-11c3-4d63-bf68-018b5087899c" />

<img width="629" height="698" alt="Screenshot 2026-10-10 142034" src="https://github.com/user-attachments/assets/4d710d40-f637-4980-a668-fb3838da435a" />

<img width="665" height="708" alt="Screenshot 2026-10-10 140059" src="https://github.com/user-attachments/assets/d36de642-d39c-46db-921e-4b011f8a3dee" />

<img width="673" height="720" alt="Screenshot 2026-10-10 140156" src="https://github.com/user-attachments/assets/29fbe543-b27a-43c6-924d-c87ffe3c6c1d" />


<img width="665" height="693" alt="Screenshot 2026-10-10 135011" src="https://github.com/user-attachments/assets/14dd7dd6-a116-4a2d-bf52-4ebe48a1542b" />


<img width="476" height="632" alt="Screenshot 2026-10-10 142154" src="https://github.com/user-attachments/assets/9d2f5369-1d6e-431d-bd4b-dd27b28c8ce5" />


<img width="651" height="523" alt="Screenshot 2026-10-11 005627" src="https://github.com/user-attachments/assets/443c4e23-4e40-4fab-8f55-fa983a95d0ca" />
