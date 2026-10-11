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
Screenshots will be added next.
