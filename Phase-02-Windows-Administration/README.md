# Phase 02 — Windows Administration & Security Analysis

## Overview

This phase focused on developing practical Windows investigation skills from a security analyst perspective. I used native Windows tools and PowerShell to examine system activity, investigate processes, analyze authentication events, and correlate evidence across multiple log sources.

The goal was not simply to identify individual events, but to understand what the activity represented, determine whether additional investigation was necessary, and document conclusions based on available evidence.

## Objectives

- Navigate and analyze Windows Event Viewer logs
- Understand Windows services and startup behavior
- Investigate running processes using PID and PPID relationships
- Build and interpret parent-child process chains
- Examine PowerShell activity and Script Block Logging
- Analyze successful and failed Windows authentication events
- Use filtering techniques to reduce log noise
- Correlate evidence across processes and Windows event logs
- Practice distinguishing expected activity from behavior requiring further investigation

 ## 1. Windows Event Analysis

I used Windows Event Viewer to examine system and security activity recorded by the operating system. I practiced navigating different log categories, identifying Event IDs, reviewing event details, and filtering large event sets to isolate relevant activity.

### Key Skills Practiced

- Navigating Windows Event Viewer
- Reviewing event timestamps, severity levels, and Event IDs
- Filtering logs by specific Event IDs
- Comparing related events based on time and context
- Separating useful security evidence from routine system noise

### Analyst Takeaway

A large number of events does not automatically indicate a security problem. Effective investigation requires filtering the available data, identifying relevant events, and using context to determine what deserves further analysis.



## 2. Windows Services Analysis

I examined Windows services to understand how background services operate and how their configuration can provide useful context during a security investigation.

I reviewed service names, descriptions, current status, and startup types to determine whether observed behavior was expected or required additional investigation.

### Key Skills Practiced

- Identifying running and stopped Windows services
- Reviewing Automatic, Manual, and Trigger Start configurations
- Using service descriptions to understand their intended purpose
- Distinguishing unfamiliar services from evidence of suspicious activity
- Evaluating services based on behavior and context rather than name alone

### Analyst Takeaway

An unfamiliar service is not automatically malicious. Service status, startup configuration, purpose, dependencies, and surrounding system activity should be considered before determining whether a service is suspicious.\

## 3. Process & Parent-Child Investigation

I investigated running Windows processes using Task Manager and PowerShell to understand how processes relate to one another. This included identifying Process IDs (PID), Parent Process IDs (PPID), command-line information, and reconstructing parent-child process relationships.

### Investigation Example

During the lab, I created and investigated the following process chain:

`explorer.exe → powershell.exe → cmd.exe`

Using PowerShell and Windows process information, I identified:

- `explorer.exe` as the parent of the PowerShell session
- `powershell.exe` as the parent of `cmd.exe`
- PID and PPID values to verify the relationships
- Command-line information to provide additional context about how processes were launched

I also executed `whoami` through the command-line chain to observe how activity could be generated and investigated.

### Key Skills Practiced

- Identifying PID and PPID values
- Reconstructing parent-child process relationships
- Reviewing process command-line information
- Distinguishing expected process relationships from unusual ones
- Using PowerShell CIM queries to investigate processes
- Recognizing the limitations of live process monitoring

### Important Observation

During the investigation, a short-lived PowerShell process terminated before I attempted to inspect it again. Because it was no longer running, it was absent from the current process list.

This demonstrated an important limitation of tools such as Task Manager: they primarily provide a snapshot of current activity. Historical logging and endpoint telemetry are necessary when investigating processes that have already terminated.

### Analyst Takeaway

Process relationships provide important context. A process such as PowerShell or Command Prompt is not inherently malicious; the parent process, command line, user context, and surrounding activity help determine whether its execution is expected or requires further investigation.


## 4. PowerShell Event Investigation

I analyzed the Windows PowerShell Operational log to investigate PowerShell activity beyond what could be observed through the live process list.

During the investigation, I reviewed several PowerShell Event IDs, including:

- **40961** — PowerShell console startup
- **40962** — PowerShell console ready for user input
- **53504** — PowerShell IPC activity associated with a process
- **4104** — PowerShell Script Block Logging

### Process and Event Correlation

I identified Event ID 53504 referencing PowerShell process ID `10488`. This PID matched a PowerShell process that I had previously observed during live process investigation.

This allowed me to correlate evidence from two different sources:

`Live Process Observation → PID 10488 → PowerShell Operational Event`

This demonstrated how process identifiers and timestamps can help connect related activity across different sources of evidence.

### Script Block Analysis

I filtered the PowerShell Operational log for Event ID 4104 and identified five Script Block Logging events.

Unlike basic process information, Event ID 4104 provided visibility into PowerShell code that had actually executed.

I reviewed script blocks involving:

- Windows language and input-profile configuration
- Registry paths associated with Windows configuration
- Windows troubleshooting functions
- Windows Error Reporting paths and cleanup operations

The scripts initially appeared unfamiliar, but their contents and behavior were more consistent with legitimate Windows configuration and troubleshooting activity than obviously malicious PowerShell execution.

### Key Skills Practiced

- Navigating PowerShell Operational logs
- Filtering logs by Event ID
- Analyzing PowerShell Script Block Logging
- Correlating process IDs between live processes and historical events
- Reviewing script behavior before assigning a security classification
- Distinguishing unfamiliar activity from evidence of malicious activity

### Analyst Takeaway

PowerShell is a legitimate administrative tool that can also be abused by attackers. Its presence alone is not enough to classify activity as malicious.

Script contents, process relationships, user context, timestamps, and surrounding events should be analyzed together before reaching a conclusion.


## 5. Windows Authentication Investigation

I analyzed the Windows Security log to investigate successful and failed authentication activity.

### Successful Logons — Event ID 4624

I filtered the Security log for Event ID **4624**, which represents a successful account logon. The initial filter returned approximately **575 events**.

I examined different logon types and learned that a successful logon does not necessarily represent a user manually signing into the computer.

Examples observed and reviewed included:

- **Logon Type 2** — Interactive logon
- **Logon Type 5** — Service logon
- **Logon Type 11** — Cached Interactive logon

I also learned to distinguish between the **Subject** and **New Logon** sections of a 4624 event.

- **Subject** identifies the security context that initiated or requested the logon.
- **New Logon** identifies the account that received the new authenticated session.

This distinction was important because the same event can contain multiple fields named `Account Name` and `Logon ID`, each representing different parts of the authentication process.

### XML Log Filtering

Rather than manually reviewing hundreds of 4624 events, I used a custom XML query to isolate successful interactive logons:

`Event ID 4624 + Logon Type 2`

This reduced approximately **575 events to 12**, significantly reducing the amount of unrelated authentication activity requiring manual review.

### Failed Logons — Event ID 4625

I then filtered the Security log for Event ID **4625**, which represents a failed logon attempt.

Two failed logon events were identified.

Both events contained the same general characteristics:

- **Logon Type:** 2
- **Caller Process:** `C:\Windows\System32\svchost.exe`
- **Caller Process ID:** `0xb58`
- **Source Network Address:** `127.0.0.1`
- **Source Port:** `0`
- **Failure Status:** `0xC000006D`
- **Account Name:** Not populated

The source address `127.0.0.1` is the local loopback address, indicating that the activity originated from the local system rather than a remote host.

Because both failed events shared the same caller process, process ID, logon type, source address, and failure pattern, the available evidence was more consistent with repeated local/system authentication activity than separate remote login attempts.

The events were therefore treated as requiring context rather than being classified as malicious solely because authentication failed.

### Key Skills Practiced

- Investigating Event IDs 4624 and 4625
- Interpreting Windows Logon Types
- Distinguishing Subject from New Logon information
- Understanding Logon IDs and Linked Logon IDs
- Filtering large Security logs
- Creating XML-based Event Viewer filters
- Examining caller process and network information
- Correlating multiple authentication events
- Making evidence-based security assessments

### Analyst Takeaway

A failed login is not automatically evidence of an attack, just as a successful login is not automatically legitimate.

Authentication events should be evaluated using the account, logon type, process information, source address, timestamps, and related events. Filtering and correlation help transform individual Windows events into useful investigative context.


## Phase 02 Summary

This phase strengthened my understanding of how Windows activity can be investigated using native system tools and security logs.

I progressed from examining individual services and processes to correlating multiple sources of evidence, including process relationships, command-line information, PowerShell Operational logs, and Windows Security events.

### Key Lessons Learned

- An unfamiliar process, service, or script is not automatically malicious.
- PID and PPID relationships help establish how processes were created.
- Parent-child process relationships provide important investigative context.
- Live process-monitoring tools have limitations because short-lived processes may disappear before they can be examined.
- Historical logs help reconstruct activity that is no longer visible in the current process list.
- PowerShell Event ID 4104 can provide visibility into executed script-block content.
- Windows authentication events must be interpreted using logon type and the correct event fields.
- Fields with similar names can represent different security contexts, making field location important during analysis.
- Filtering large datasets is more effective than manually reviewing every event.
- Multiple pieces of evidence should be correlated before classifying activity as suspicious or benign.

### Phase Outcome

By the end of this phase, I was able to use Windows-native tools to perform basic security investigations, reduce log noise, reconstruct process relationships, analyze PowerShell activity, investigate authentication events, and document conclusions based on observed evidence.

These skills provide the Windows analysis foundation for the next phase of the lab, which will focus on network activity and additional endpoint telemetry.
