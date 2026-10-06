<h1>Evidence Note: SC-7-001</h1>

- <b>Evidence ID:</b> SC-7-001
- <b>Control:</b> SC-7, Boundary Protection
- <b>Date performed:</b> 2026-10-06
- <b>Performed by:</b> Preston Cheriyan
- <b>Artifact:</b> SC-7-001_lab-network-boundary_2026-10-06.png

<h2>Objective</h2>

Establish an isolated lab network with controlled outbound internet access and no direct exposure to the host's physical network, and verify it does not conflict with the host VPN.

<h2>Method</h2>

A legacy internal switch (NATSwitch) and NAT network (NATNetwork, 192.168.10.0/24) from a previous lab were identified and removed prior to configuration, after confirming no VMs were attached. Hyper-V default VM and virtual disk paths were set to the lab directory. An internal Hyper-V switch (LabSwitch) was created, the host was assigned 10.10.10.1/24 on the switch interface as the lab gateway, and a Windows NAT network (LabNAT) was created for 10.10.10.0/24. Configuration was verified from an elevated PowerShell session with NordVPN connected, bracketed by `Get-Date` timestamps (12:16:59 AM to 12:17:00 AM).

<h2>Results</h2>

| Check | Expected | Result |
|---|---|---|
| Hyper-V default paths | Lab VMs and VHDs directories | Pass |
| LabSwitch type | Internal | Pass |
| Gateway address | 10.10.10.1/24, Preferred | Pass |
| LabNAT | 10.10.10.0/24, Active | Pass |
| Route overlap with host VPN | No overlap between lab and NordLynx routes | Pass |
| Lab traffic path with VPN connected | vEthernet (LabSwitch), 10.10.10.0/24 | Pass |

<h2>Limitations</h2>

- Inbound protection is based on the design behavior of an internal switch with NAT. Unsolicited inbound connection attempts were not actively tested.
- The NAT does not filter outbound traffic. Lab VMs can reach any internet destination, and their traffic exits through the host's active connection, including the VPN tunnel when connected.
- The host has direct access to all lab systems and is therefore inside the lab's trust boundary. A compromise of the host would extend to the lab.
- No VMs existed at the time of this check. End-to-end connectivity will be validated once DC01 is built.

<h2>Conclusion</h2>

Lab network boundary established and verified. Host VPN confirmed non-conflicting. Ready for VM builds.