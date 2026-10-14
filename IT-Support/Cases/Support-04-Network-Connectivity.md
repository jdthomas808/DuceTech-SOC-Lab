# Support-04: Network Connectivity Troubleshooting

**Environment:** DuceTech Windows 11 VM, VMware Workstation, NAT networking  
**Account:** Jordan.Davis — standard user  
**Status:** Simulated network fault resolved; separate VM instability unresolved

## Objective
Identify a disconnected network adapter, restore its connection, and verify gateway and website access.

## Working Baseline
- IPv4 address: 192.168.243.128
- Default gateway and DNS server: 192.168.243.2
- DHCP enabled.
- Gateway ping: 4 replies, 0% packet loss.
- External IP ping (1.1.1.1): 4 replies, 0% loss.
  The first reply took 1,425 ms; the remaining replies took 36–71 ms.
- DNS lookup for www.microsoft.com. returned IP addresses.
- Microsoft website loaded in Chrome.

## Controlled Fault
Unchecked Connected for the VM's network adapter in VMware settings.

This simulated an unplugged network cable inside the VM.

## Diagnosis
Ran:

    ipconfig /all

Ethernet0 reported:

    Media State: Media disconnected

This identified an inactive network link. The known cause in this
exercise was the deliberately disconnected virtual adapter.

## Corrective Action
Rechecked Connected for the VM's network adapter.

## Verification
A VM crash interrupted the initial verification attempt.
After Windows restarted:

- Ping to 192.168.243.2 returned 4 replies with 0% packet loss,
  with each reply taking less than 1 ms.
- The Microsoft website loaded in Chrome, although slowly.

These checks confirmed connectivity after reconnection and reboot.
They do not establish whether connectivity recovered before the crash.

## Separate Outstanding Issue
The VM has recurring unexpected restarts under investigation.
The network exercise did not resolve or establish the cause of
those crashes or the slow website load.

## Evidence
- Working network configuration and baseline tests.
  <img width="1110" height="610" alt="Screenshot 2026-10-14 131315" src="https://github.com/user-attachments/assets/2d1c92f0-0258-4c26-b47a-925d37dfb2ad" />

- Ethernet0 showing Media disconnected.
  <img width="1107" height="633" alt="Screenshot 2026-10-14 181223" src="https://github.com/user-attachments/assets/a3ccae17-d838-456e-bd71-7aa98f52fab7" />

- Successful gateway ping after recovery & Microsoft webpage loaded after recovery.
  <img width="1714" height="940" alt="Screenshot 2026-10-14 182701" src="https://github.com/user-attachments/assets/9f72bdb7-d088-4302-8d18-4a2bec3949ec" />


## Lesson Learned
Check the network link and IP configuration before investigating DNS.
After restoring the link, verify both gateway reachability and
user-facing website access before closing the network issue.
